# Write once run anywhere with nw js and Cordova

## Cordova
Open source project built by Apache.
Provides two main things:
* toolchain that builds a mobile app wrapper using html5/css/js
* native access to the platform via plugins (js api shim)

```
cordova create cordova bla.app App
```

Add platforms:

```
cordova platform add ios android windows --save
```

Add plugins:
```
cordova plugin add cordova-plugin-whitelist cordova-plugin-statusbar cordova-plugin-splashscreen cordova-plugin-geolocation cordova-plugin-camera cordova-plugin-crosswalk-webview --save
```

## NW.JS
Sponsored by the intel software lab.
Build on top of node-webkit.

Allows to build full-blown desktop apps with access to the native platform via any node module.

Needs a package.json file:

```
{
    "name": "Bla",
    "version": "1.0.0",
    "main": "www/index.html",
    "windows": {
        "title": "Bla! Desktop",
        "toolbar": false,
        "resizable": true,
        "fullscreen": false,
        "width": 1024,
        "height": 768
    }
}
```

Workflow:
* gulp task to build
* nw .: takes the nw application with the current folder
