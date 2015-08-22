# Configuring local SSH access in iOS 7+

- in iOS 7+ the kernel doesn't allow unprivileged apps (i.e. ones running as `mobile`, not `root`) to access ports < 1024.
	+ You can hack around this by moving a SSH client app to /Applications, but that breaks App Store upgrades, so fuck it
	+ Better way: edit `/etc/services` and add an unpriviliged port to use for SSH, ex: 
	```
	ssh2	6022/udp
	ssh2	6022/tcp
	```
	+ However since `launchd` manages the SSH daemon, `/etc/services` isn't enough, you need to edit `/Library/LaunchDaemons/com.openssh.sshd.plist` as well to listen on an alternate port

- Under the `Listeners` key in `/Library/LaunchDaemons/com.openssh.sshd.plist`, add:
```
<key>Alternate Listeners</key>
<dict>
	<key>SockServiceName</key>
	<string>ssh2</string>
</dict>
``` 
- Now reboot and SSH will be listening on both port 22 and whatever port you specified, as long as the alternate port is >1024 you'll be able to SSH in!


