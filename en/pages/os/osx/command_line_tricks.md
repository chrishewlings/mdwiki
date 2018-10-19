Command Line Tricks for OS X 
================

System Administration
---------

#### Check system version without running MRI

```bash
$ sw_vers
```

n.b. on 10.9+, you need to run the following beforehand, if in SUM:
```bash
$ launchctl load /System/Library/LaunchDaemons/com.apple.kextd.plist
$ launchctl load /System/Library/LaunchDaemons/com.apple.configd.plist
```
------
#### Check Serial number without running MRI

```bash
$ system_profiler SPHardwareDataType
```
n.b. On 10.9+, you also need to run the same commands as above.

------

#### Prompt user to reset password on next login

- Enable root user, then:

```bash
$ pwpolicy -a root -u $user_to_reset -setpolicy "newPasswordRequired=1"
```
------

#### Create a new user from command-line (Or Single User Mode)

Hint: n.b. If in SUM, run:
	- for 10.4-10.6 : `launchctl load /System/Library/LaunchDaemons/com.apple.DirectoryServices.plist"`
	- for 10.7+ : `launchctl load /System/Library/LaunchDaemons/com.apple.opendirectoryd.plist"`

then:

```bash
# dscl . -create /Users/$username
# dscl . -create /Users/$username UserShell /bin/bash
# dscl . -create /Users/$username RealName "Lucius Q. User"
# dscl . -create /Users/$username UniqueID "1010"
# dscl . -create /Users/$username PrimaryGroupID 80
# dscl . -create /Users/$username NFSHomeDirectory /Users/$username
```

You can then use passwd to change the user's password, or use:

```bash
# dscl . -passwd /Users/$username password
```

Create /Users/$username for the user's home directory and change ownership so the user can access it, and be sure that the UniqueID is in fact unique.
```bash
# mkdir /Users/$username
# cp -r "/System/Library/User Template/English.lproj/" /Users/$username
# chown -R luser:staff /Users/$username
```

of course, replacing `$username` with the username of your choice. 

------

#### Make a complete, bootable copy of a drive or partition with `rsync` (like SuperDuper)

Warning! this will remove any files that are on the destination drive!

```bash
$ rsync -xrlptgoEv --progress --delete /Volumes/$SOURCE /Volumes/$DESTINATION
```
replacing `$SOURCE` and `$DESTINATION` respectively.

-------

#### Make a disposable ramdisk

```bash
$ hdiutil attach -nomount ram://$RAMDISKSIZE
``` 
Tip: This will return a drive ID, like `/dev/disk2`, to be used in the next command
- n.b. `$RAMDISKSIZE` should be given in quantity of 512kb sectors

```bash
$ diskutil eraseVolume hfs+ $DRIVEID
``` 
This will partition the ramdisk to be usable by OS X

--------

#### Reveal forgotten automatic login password

```bash
$ sudo ruby -e 'key=[125,137,82,35,210,188,221,234,163,185,31];IO.read("/etc/kcpassword").bytes.each_with_index{|b,i|break if key.include?(b);print [b^key[i%key.size]].pack("U*")}'```

--------

#### Using Keychain to manage SSH keys

`ssh-add` command allows you to save your private key file to the keychain instead of using `~/.ssh/`
- Example:
- `$ ssh-add -k keyfile`
- `$ ssh $servername` should now use the key instead of asking for password.

--------



Troubleshooting
---------

#### Start user login without launching GUI
- On login screen, select `Other...`
- enter `>console` as the username and press enter.

-------

#### Find all apps that have been installed from the Mac App Store

```bash
$ mdfind "kMDItemAppStoreHasReceipt=1"
```

------

#### Trackpad not scrolling after migration?

```bash
$ defaults delete .GlobalPreferences com.apple.trackpad.scrollBehavior
```

------

#### Can't find original image used for desktop?

```bash
$ defaults write com.apple.dock desktop-picture-show-debug-text -bool TRUE; killall Dock
```

------

#### Change keyboard layout at login screen

- The .plist connector that controls the keyboard layout is `/Library/Preferences/com.apple.HIToolbox.plist`, but it's in binary format. 
- Easiest way to convert:
	+ ` $ plutil -convert xml1 com.apple.HIToolbox.plist`
	+ And then remove the offending keyboard layout.  They use numeric integer codes for selection, so the easiest way to find the right one is to configure it in the user, and then convert/copy `~/Library/Preferences/com.apple.HIToolbox.plist` to `/Library/Preferences/`

------

#### Shrink fussy Parallels disks

- First, boot into the VM and zero out free space on the virtual disk. `zerofree` can do this for Linux.
- Then: 
`$ prl_disk_tool compact --buildmap --hdd $path_to_virtual_disk/`

Warning! The trailing slash is important. 
Note: the `--buildmap` option checks unsupported filesystems for free space to compact. Otherwise it'll return with no change.


Scripting
----------

#### Scripting Fast User Switching

##### Go to login window without logging out:
```bash
$ /System/Library/CoreServices/Menu\ Extras/User.menu/Contents/Resources/CGSession -suspend
```

##### Go to another user without logging out:
```bash
$ /System/Library/CoreServices/Menu\ Extras/User.menu/Contents/Resources/CGSession -switchToUserID $UID_OR_SHORTNAME
```


#### Changing nested plist values

```
$ /usr/libexec/PlistBuddy -c "set :$key:$subkey1:$subkey2:$subkeyn $value" $plistfiletochange
```

#### Remaining Battery percentage in terminal
`pmset -g batt | egrep "([0-9]+\%).*" -o --colour=auto | cut -f1 -d';'`

#### Current display resolution
`system_profiler SPDisplaysDataType | \grep Resolution | cut -c 11-`

#### CPU + RAM info
##### Physical cores
`sysctl -n hw.physicalcpu`
##### Logical cores
`sysctl -n hw.logicalcpu`
##### Quantity of RAM (in GB)
`echo "$(($(sysctl -n hw.memsize)/1073741824))"`

#### Show all IP addresses

`for iface in $(ifconfig -lu); do IP=$(ipconfig getifaddr $iface); [[ "$?" -eq 0 ]] && printf "$iface:\t$IP\n"; done`

## Misc

#### Scan available access points

`/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -s`

#### generate random password

`openssl rand -base64 $LENGTH`

#### convert clipboard content to plaintext

`pbpaste | textutil -convert txt -stdin -stdout -encoding 30 | pbcopy`

#### Relaunch Finder as root

+ <=10.9:
	`sudo /System/Library/CoreServices/Finder.app/Contents/MacOS/Finder 2>&1`
+ >=10.10
	`sudo login -f root /System/Library/CoreServices/Finder.app/Contents/MacOS/Finder 2>&1`

#### Quit Finder and don't relaunch it:

`osascript -e 'tell application "Finder" to quit'`

#### Write to syslog

`echo "hello" | logger`

#### Automount drives without having a user logged in <`/Library/Preferences/SystemConfiguration/autodiskmount.plist`>:
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>AutomountDisksWithoutUserLogin</key>
    <true/>
</dict>
</plist>
```

#### add a spacer to the dock
`defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="spacer-tile";}' `

#### time since last user input
```
echo $((`ioreg -c IOHIDSystem | sed -e'/HIDIdleTime/ !{ d'-e't'-e'}'-e's/.* = //g'-e'q'` / 1000000000))
```

#### Files in `/var/db`

|File|Description|
|----|-----------|
|`.AppleSetupDone`|Created on completion of Setup Assistant. Remove to skip login window and create a new admin account.|
|`.RunLanguageChooserToo`|If exists, allows user to change language of Setup Assistant, otherwise it follows the installer language|