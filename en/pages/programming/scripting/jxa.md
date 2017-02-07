#jxa

## Useful boilerplate

### For almost everything

- `Application.currentApplication().includeStandardAdditions = true` -- adds OSA standard additions, adds chooseFile, stuff like that.

- So many useful things: [JXA Cookbook](https://github.com/dtinth/JXA-Cookbook)

## Applications

###Accessing applications:

by name, bundleId, PID, or path
`Application('Mail'), Application('com.apple.mail'),Application('/Applications/Mail.app')`

###getting app running script
`Application.currentApplication()`


### Object properties

```
Mail = application('Mail')
Mail.name() => returns 'Mail'
```

Same syntax used for arrays of items, ex.
```
var frontWindow = Mail.windows[0]
frontWindow.name()
```



## Talking to Cocoa

- `$` operator is used to talk to Cocoa
- ex.
`var cocoaStrPath = $("~/Pictures").stringByExpandingTildeInPath`

``` var imageFrame = $.NSMakeRect(400,400, width, height)```
gives an NSString with the full POSIX path
- Converting POSIX path to file reference :
	- `fileRef = Path("<POSIXPATH>")`

##Misc

- Interactive JXA

`osascript -l JavaScript -i`

### Progress bar
```
Progress.description =  "A simple progress indicator"
//Progress.additionalDescription = "Preparing…"
delay(2)
Progress.totalUnitCount = 100;

for (var i = 1; i < 101; i++) {
    Progress.additionalDescription = "I am on step " + i
    Progress.completedUnitCount = i
    delay(0.1)
}
```


## Cocoa/ObjC Bridge

- `ObjC.import('Cocoa')` -- brings in Cocoa framework , required for all examples

### Ask Cocoa to make a window

```
var height = 400
var width = 400


var window = $.NSWindow.alloc.initWithContentRectStyleMaskBackingDefer(
  $.NSMakeRect(0,0,width, height),
  $.NSTitledWindowMask | 
  $.NSResizableWindowMask, 
  $.NSBackingStoreBuffered,
  false
 )
 
 var imageView = $.NSImageView.alloc.initWithFrame($.NSMakeRect(0,0, width, height))
 
 window.center
 window.makeKeyAndOrderFront(window)
```

### Send a notification 

```
var notification = $.NSUserNotification.alloc.init;
notification.title = "Hello";
notification.informativeText = "World";
notification.soundName = $.NSUserNotificationDefaultSoundName;
notification.actionButtonTitle = "Acknowledge";

$.NSUserNotificationCenter.defaultUserNotificationCenter.deliverNotification(notification);
```

### Subshell
```
var task = $.NSTask.alloc.init;
task.launchPath = "/usr/bin/say";

var args = ["-v", "Vicki", "The orangutans have taken over the car wash. Bring some pajamas."];

// $() converts a JS array to an NSArray
task.arguments = $(args);

task.launch;
```
### Logging 

``` 
// Use %@ as format string.
// You can also pass an array instead of a string/number.
var age = 29;
$.NSLog("I am %@ years old.", age);
``` 




