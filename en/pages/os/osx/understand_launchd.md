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




