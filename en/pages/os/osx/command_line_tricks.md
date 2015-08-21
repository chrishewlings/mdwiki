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
