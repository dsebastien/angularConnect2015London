# Building Native Mobile Apps with NativeScript

## NativeScript
A way to write JavaScript to build mobile applications with a native UI.
A bit like PhoneGap and Ionic BUT the components are native ones.
A bit like Xamarin but there isn't cross-compilation; code stays JS.

NativeScript also supports developing Web applications.

Integrates nicely with Angular 2.


## Why NativeScript?
* skills reuse: JS, CSS and Angular 2
* code reuse: npm modules, 3rd party iOS and Android libraries
* easily use native APIs
  * no wrappers to access native APIs
  * use native UI elements

## Basic examples

```
// Android
var time = new android.text.format.Time();
time.set(1, 0, 2015);
console.log(time.format("%D"));

// iOS
var alert = new UIAlertView();
alert.message = "Hello world!";
alert.addButtonWithTitle("OK");
alert.show();

```

## Type conversion service
NativeScript embeds a type conversion service to convert between NativeScript JS code and types to native types. This, in combination with their Metadata and Call Dispatcher make it possible to easily invoke native APIs

## Modules
```
var fileSystemModule = require("file-system");
new fileSystemModule.File(path);
```

## Templates
With NativeScript, templates are written using XML.
