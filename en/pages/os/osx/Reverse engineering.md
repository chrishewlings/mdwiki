# Reverse engineering

- the static, hard-coded key to encrypt Mac App Store binaries is apparently `ourhardworkbythesewordsguardedpleasedontsteal(c)AppleC`

## Old (10.4-ish era) boot process

### EFI

- SMC gets signaled by power button or another source and powers the CPU and chipset
- Low level firmware performs POST, talks to northbridge & southbridge and initializes hardware.
- Firmware passes control over to EFI, and starts accepting keystrokes for startup key sequences. 
- If nothing is pressed, EFI queries NVRAM for the configured boot device. If none is configured, the EFI then queries available devices for EFI executables. 
- When an appropriate EFI executable is found, (usually `/System/Library/CoreServices/boot.efi`) the EFI passes control over to it and then bootstraps the kernel.

### Kernel space startup

- Various Mach/BSD data structures are initialized by the kernel.
- The I/0 Kit is initialized.
- The kernel starts `/sbin/machinit`, the Mach service naming (bootstrap) daemon. `machinit` maintains mappings between service names and the Mach ports that provide access to those services.

### User space startup

- `machinit` starts `/sbin/init`, the traditional BSD `init` process. `init` determines the runlevel, and runs `/etc/rc.boot`, which sets up the machine enough to run single-user.
- During its execution, `rc.boot` and the other rc scripts source `/etc/rc.common`, a shell script containing utility functions, such as `CheckForNetwork()` (checks if the network is up), `GetPID()` , `purgedir()` (deletes directory contents only, not the structure), etc.
- `rc.boot` figures out the type of boot (Multi-User, Safe, CD-ROM, Network etc.). In case of a network boot (the sysctl variable kern.netboot will be set to 1 in which case), it runs `/etc/rc.netboot` with a start argument.
- `/etc/rc.netboot` handles various aspects of network booting. For example, it performs network and (if any) local mounts. It also calls `/usr/bin/nbst` to associate a shadow file with the disk image being used as the root device. The idea is to redirect writes to the shadow file, which hopefully is on local storage.
- `rc.boot` figures out if a file system consistency check is required. Single-user and CD-ROM boots do not run fsck. SafeBoot always runs `fsck`. `rc.boot` handles the return status of `fsck` as well.
- If `rc.boot` exits successfully, `/etc/rc`, the multi-user startup script is then run. If booting from a CD-ROM, the script switches over to `/etc/rc.cdrom` (installation).
- `/etc/rc` mounts local file systems (HFS+, HFS, UFS, /dev/fd, /.vol), ensures that the directory `/private/var/tmp` exists, and runs `/etc/rc.installer_cleanup`, if one exists (left by an installer before reboot).
- `/etc/rc.cleanup` is run. It "cleans" a number of Unix and Mac specific directories/files.

## Finder behaviour

### Hiding files

- There are four methods to hide files from the Finder. 
	+ On an HFS+ volume, `SetFile` can be used to flip the invisible bit.  This is the Classic Mac OS way to hide a file.
	+ Adding a dot before the name of the file. This is the classic POSIX convention for hidden files.
	+ The third method resembles the second – if a file named `.hidden` exists in a directory, with a newline separated list of files, the items listed in the `.hidden` file will not appear in Finder. 
	+ Lastly, the `chflags` command can be used to assign the flag `hidden` or `nohidden`.  This _may_ be the same as flipping the invisible bit since the resource fork has been deprecated from some time.
	
## Startup jobs

n.b. Found on MR forums. some of these are _OLD_. Like Tiger era. Needs testing.

"A more complete list, roughly in order of being launched on an auto-login system:

1. /etc/mach_init.d/
2. /etc/rc/ and /etc/rc.local - totally unsupported, and not created by default (but probably still work)
3. LaunchDaemons (run at system startup, default to root user) in /Library/LaunchDaemons and /System/Library/LaunchDaemons (possibly /Network/Library/LaunchDaemons, but I don't know)
4. /etc/mach_init_per_login_session.d/ and /etc/mach_init_per_user.d/
5. (old) /Library/StartupItems, /Network/Library/StartupItems, /System/Library/StartupItems - probably does not work anymore
6. cron launched @reboot items (yes, cron is still there), this might even work for everyone's crontabs
7. /Library/Security/SecurityAgentPlugins that have been loaded by being listed in the proper spots in /etc/authorization
8. /private/var/root/Library/Preferences/com.apple.loginwindow.plist, in the LoginHook key (runs as root, passed the username)
9. MCX (WorkgroupManager) login hooks (runs as root, but passed the username)
10. note: below this network home directories are more reliably available, as is a connection to the WindowsServer
11. LaunchAgents (run at login, generally in the user's space) in ~/Library/LaunchAgents, /Library/LaunchAgents, /Network/Library/LaunchAgents and /System/Library/LaunchAgents
12. MenuBar items from ~/Library/Preferences/com.apple.systemuiserver.plist and /Library/Preferences/com.apple.systemuiserver.plist (+MXC added items)
13. /Library/Preferences/loginwindow.plist, in the key (array of paths) AutoLaunchedApplicationDictionary (everyone gets this launched at login, runs as user) (+MXC added items)
14. LoginItems (generally GUI items) ~/Library/Preferences/com.apple.loginitems.plist and possibly /Library/Preferences/com.apple.loginitems.plist (have not tried) (+MXC added items)"
 
