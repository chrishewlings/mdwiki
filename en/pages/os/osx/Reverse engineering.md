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