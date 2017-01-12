#jxa

## Applications

###Accessing applications:

by name, bundleId, PID, or path
Application('Mail'), Application('com.apple.mail'),Application('/Applications/Mail.app')

###getting app running script
Application.currentApplication()

## Object properties

```
Mail = application('Mail')
Mail.name() => returns 'Mail'
```

Same syntax used for arrays of items, ex.
```
var frontWindow = Mail.windows[0]
frontWindow.name()
```

Useful things:

`ObjC.import('Cocoa')` -- brings in  Cocoa framework 
`Application.currentApplication().includeStandardAdditions = true` -- adds OSA standard additions, basically boilerplate.
	- adds chooseFile, stuff like that

## Talking to Cocoa

- `$` operator is used to talk to Cocoa
- ex.
`var cocoaStrPath = $("~/Pictures").stringByExpandingTildeInPath`

- ex2. (window boilerplate)

```
ObjC.import('Cocoa')

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

``` var imageFrame = $.NSMakeRect(400,400, width, height)```
gives an NSString with the full POSIX path
- Converting POSIX path to file reference :
	- `fileRef = Path("<POSIXPATH>")`

##Misc

- Interactive JXA

`osascript -l JavaScript -i`
