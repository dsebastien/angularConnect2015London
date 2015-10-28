# Building cross-platform apps with Ionic

## Links
* alpha: ionic.io/2

## Ionic Stats
* top 40 OSS project
* 1+M apps
* ...

## About Ionic
* mobile only UI toolkit

## About Ionic 2
* evolution of the Ionic framework for Angular 2
* same framework
* same goals
* supports better navigation
* supports theming
* has tons of built-in icons
* integrates usage of Web Animations API

## Simplicity

### Component model
```
  <button>...</button>
  <ion-checkbox>...</ion-checkbox>
  <ion-list>
    <ion-item>...</ion-item>
  </ion-list>
```

```
@Page({
    templateUrl: 'profile.html'
})
export class Profile{
    constructor(){
        this.first = 'Biff';
        this.last = 'Tannen';
}
```

App: `@App` decorator

### Platform continuity
* iOS: Android
* One code base
* Same HTML and JS
* More than just different CSS
* content gets adapted to the device/platform

### Icons
* ~900 icons (SVG)
* ...

### Navigation
* navigation not tightly coupled to the URL
* better UI router integration
* push/pop navigation
  * similar to iOS/Android
  * full control of the navigation experience
  * URL and deep-linking support

```
pushSettings(){
    this.nav.push(Settings);
}

goBack(){
    this.nav.pop();
}
...
```

### Theming
* colors and variables
* easy to customize for your brand

### Animations
Web animations API (W3C draft): browser's animation engine,
* not available yet for Edge, IE, ... (limited support)

### JavaScript
Ionic 2 built with ES2015 & TypeScript.

### Native power
* easy access to native functionality

## IONIC CLI
* ES6/TypeScript transpilation
* Sass compiling
* Cordova build
* Webpack bundling
* Scaffolding/architecture
* ...

## Future
* Web Worker support
* Staying in sync with Angular 2
* Add even more to ionic.io services
