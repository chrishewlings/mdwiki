
#Cocoa with Swift Essential Training

## Swift/Cocoa basics
- declare variables with keyword `var`
	- no semicolon is necessary to terminate statements
	- datatypes are inferred generally, but can be forced with the syntax `var_name:type`

- basic types
	- `Int`
	- `Float`
	- `Bool`

- constants are declared using keyword `let` instead of `var`

# What is Cocoa?
- All of the IDEs, SDKs, APIs, libraries, and runtimes that comprise the development layer of ObjC & Swift.
	- Cocoa refers to Mac development
	- Cocoa Touch refers to iOS development

## functions

- functions are declared with `func myFunction () { BLOCK }`
- functions default to returning `void`
- to return a value, the syntax `func myFunction () -> *type* { BLOCK } ` is used

- parameter values can be declared inline, as in `func myParam(p1:NSInteger, p2:String) { BLOCK }`

## Arrays

- declared like variables
- `var myArray:Array = [a,b,c]`
- call specific values with `myArray[*n*]` syntax

## dictionaries

- similar declaration as arrays, but with key/value pairs
- `var myDictionary:Dictionary = ["Chris":"me", "Donuts":"Delicious"]
- `myDictionary.count`, `mydictionary.erase` are common operations

## classes

defined as `class CustomClass : *nameOfParent*` to establish inheritance

## control flow

#### if/else

`if (false) {
	var myString:String = "condition is true!"
}
else if ( 1 == 1) {
	"condition is false"
}
else {
	"who knows"
}`

#### for loops

- familiar syntax.

`for(var i:Int = 0; i < 10; i++) {
	i
}` *n.b. parens are optional*

cool shortcuts:

`for i in 1...100 {
	i
` is proper syntax to execute from 1 to 100

loop through arrays:

`var a:Array = [1,2,3]`
`for num in a {
	num
}`

## basics of XCode

#### layout
- left pane is the __navigator__
	- __project navigator__ contains the file hierarchy of your project
- center pane is __editor__
- right pane is *context sensitive* and contains a number of functions
	- for example, opening a code file vs a user interface file will show different options

#### Model View Controller
- MVC is a design pattern
- Not unique to Cocoa or Swift
- Core principle: Keep visual content separate from your data
- Encouraged, but not enforced

Model | Controller | View
------|------------|-----
Data | code | user interface

__Data__ can be sent to the __controller__ to update the __view__

*.xib* files are used for UI
*.swift* files are for code and data

- a UI element can be defined as an __outlet__ or __action__ (or others) to send/receive events from the __controller__

#### Basic interaction *(see BasicInteraction.xcodeproj)*
- __Attributes Inspector__ in the right pane shows properties specific to the selected UI element
- initialize a UI outlet in code:
	- `@IBOutlet weak var *var_name*: *type*!`
- initialize a UI method in code:
	- `@IBAction func *something(sender:AnyObject)*`	

- use a variables' value inside a string:
	- `var name = "something"`
	- `"Hi \(name)!`

#### shortcut to connecting .xib elements to code *(see QuickConnections.xcodeproj)*

- the __Assistant Editor__ allows us to quickly create IBOutlets from UI elements via `Ctrl-(drag mouse)`

##### sidebar about variable scope and strength
- __weak__ & __strong__ are used for memory management to define the ownership or responsibility for elements.
	- in swift, subview elements like labels and buttons that are subviews of a window are __strong__, so they are owned by the *.nib*
	- therefore, when we define any connections, we want to define them as __weak__.
	- the `!` mark is called an *implicitly unwrapped optional*.  That means that the value can be `nil` at some point without issue. In Swift, any datatype can have a `nil` value. 
		- a `?` indicates that it is __optional__. this indicates that the variable is wrapped up in a 'package'
		- in order to access the value of the variable you need to 'unwrap' the package using a `!` on the variable named when referred to. 

## Cocoa Application lifecycle *(see `AppLifecycle.xcodeproj`)*
- NSApplicationMain() makes UIApplication instance
- NSApplicationMain() gets info from Info.plist about `.xib` file to load
- NSApplication instance handles main loop
- App-level events are handled by delegation
	- our AppDelegate is connected to our NSWindow/NSView/other UI elements
	- we edit `AppDelegate.swift` and not `main.swift`, basically.

### Diagnosing connection issues *(see `DiagnosingConnections.xcodeproj`)*

- Xcode automatically pauses and launches debugger when app crashes
- check for empty circles next to app labels in `@IBOutlet` declarations
- ensure that outlets are not defined as actions and vice vesa

### Custom controller *(see `CustomController.xcodeproj`)*

- define a custom class and control its behavior w/r/t your UI using the __Identity Inspector__

### creating alerts *(see `CreatingAlerts.xcodeproj`)*

- a __panel__ is a popup window
- a __sheet__ is an extension of the existing panel

#### common
- `NSAlert` is the base class
- `NSAlert.messageText` can be defined to whatever you want to show

##### alert window (panel)

- `NSAlert.runModal()` invokes the window

##### alert sheet (foldout)
- `NSAlert.beginModalSheetForWindow()`, where a *completion handler* can be defined to return a value to the application indicating something happened
- `NSAlert.addButtonWithTitle()` gives a button with the ability to return a value, defined in the `NSAlert` class


### Delegation
- Act on behalf of another object
- Sometimes user for event handling
- Can be used for callbacks
- Can also be used similar to inheritance

####Example:
- `NSApplication` contains the main loop
- `AppDelegate` class performs tasks on behalf of `NSApplication`

#### Workflow for Delegation
- Define the protocol, or use existing protocol
- Declare protocol adoption
- Set instance as a delegate, if necessary.
- Handle required methods
- Handle optional methods as needed

- Supporting protocols can be added to a class with comma separated values after the name of the parent class, e.g.

`class AppDelegate: NSObject, NSApplicationDelegate, someNewProtocol`

- handling new events in code can be added to the skeleton of the AppDelegate class using a function, like `applicationDidFinishLaunching` and `applicationWillTerminate` are predefined by XCode

#### Delegation with respect to UI *(see `DelegationUI.xcodeproj`)*
- things can be defined as delegates by the __Connection inspector__ and by following the name of the superclass in the AppDelegate declaration with the class we want to delegate.

end chapter 4.
