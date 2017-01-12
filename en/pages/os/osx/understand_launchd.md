# Startup processes

## LaunchAgents/LaunchDaemons

`launchd` runs LaunchDaemon `.plist` files in several different paths:

Without GUI:
------------

- `/System/Library/LaunchDaemons` (LaunchDaemons installed for _all users_ by *the OS*)
- `/Library/LaunchDaemons` (LaunchDaemons installed for _all users_ by the *system administrator*)


With or without GUI:
--------------------

- `/System/Library/LaunchAgents` (LaunchAgents installed for _all users_ by the *OS*)
- `/Library/LaunchAgents` (LaunchAgents installed for _all users_ by the *system administrator*)
- `~/Library/LaunchAgents` (LaunchAgents installed for _one user_)

- LaunchDaemons can be overrided or disabled by two mechanisms:
	+ adding a special key to the services' startup file (e.g. `/System/Library/LaunchDaemons/com.apple.telnet.plist`:

````
<key>Disabled</key>
	</true>
````

	+ adding a similar argument to the `/private/var/db/launchd.db/com.apple.launchd.overrides.plist` to disable for _all users_
````
<key>com.apple.FileServer</key>
<dict>
	<key>Disabled</key>
	<true/>
</dict>
````

	+ adding the same as above, but to `/private/var/db/launchd.db/com.apple.launchd.peruser.$UID/overrides.plist` will override/disable the LaunchDaemon but only for the user specified in `$UID` 

## LoginHook

````
# defaults write com.apple.loginwindow LoginHook /path/to/script
````

Note: This differs from a login item -- a LoginHook (or LogoutHook) is run at _every_ users' login/logout, not just a specific one.  It also runs as the root user, not as the user logging in. 


## Reverse engineering launchd

- `launchctl bootshell` , since 10.10 or 10.11

	+ Starts system to shell but places restrictions on XPC `(XPC_NULL_BOOTSTRAP)`

- Networking and whatnot work but anything relying on XPC doesn't. user login/DS/etc are inaccessible ; seems like it's essentially a chroot but doesn't actually prevent actual file level manipulations. 


- Thoughts:
	+ reverse what it's doing via lldb or simply checking for added flags in /var/db/com.launchd.xpcd/ 
	+ Launchd code is no longer available open source since Yosemite, so no luck there. 
	+ Continuing to normal boot can be done with launchctl bootshell continue

## Changes to `launchctl` since Yosemite


`# cat ~/Library/LaunchAgents/org.company.test.plist`

```
<plist version="1.0">
    <dict>
    <key>Label</key>
        <string>org.company.test</string>
            <key>ProgramArguments</key>
                <array>
                        <string>/usr/bin/env</string>
                 </array>
            <key>RunAtLoad</key>
                 <true/>
            <key>StartCalendarInterval</key>
                <dict>
                  <key>Hour</key>
                      <integer>0</integer>
                  <key>Minute</key>
                      <integer>0</integer>
                 </dict>
    </dict>
</plist>
```

- Different launchd sessions (since 10.10)
	- `user/$UID` is the *background* session. Needs `LimitLoadToSessionType=Background`.
	- `gui/$UID` is the *Aqua* session.  

- `bootstrap` is to load a file into a given domain
- `kickstart` is to force running a job, ignoring its configured run condition.

