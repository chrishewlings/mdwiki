# run through key value matches in a dict
```
for k,v in something.items():
	print(k,v)
```

# globbing paths
```
import glob
osx_install = glob.glob("/Applications/" \ "Install*OS*X.app")

print(osx_install)
['/Applications/Install Mac OS X Lion.app', '/Applications/Install OS X Mountain Lion.app']
```

# version numbers

`distutils.version` has `LooseVersion` and `StrictVersion` objects useful for comparing version values

# logging to console

```
import syslog
syslog.openlog("TEST") // uses TEST as name of app writing to log
syslog.syslog(syslog.LOG_NOTICE, "Something") // LOG_NOTICE is the logging level
syslog.closelog()
```
