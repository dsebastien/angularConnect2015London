# Modularity and packaging for Angular2 applications

## ES6 Module
* standardized
* clear sync/async semantics
* problem with loading: where to get from, what is the extension, ...

## Module loader
* removed from the ES2015 spec
* spec worked upon in whatwg: https://whatwg.github.io/loader

## Setting up build and packaging

### Discussion
* options?
* tradeoffs?

### Transpiler
Babel vs TypeScript

### Module format
CommonJS vs System.register

SystemJS:
* module loader
* 'super' polyfill
* defines the System object. System.JS
* correct ES2015 semantic
* support for circular dependencies
* easy to package / pre-load
* insanity warning
  * System.import loader from the (old) specification
  * System.register module format
  * SystemJS loader
  * SystemJS bundler (JSPM)

CommonJS:
* more familiar to JS devs
* more compact, small overhead
* more tooling


## Angular 2
* SystemJS loader
* angular2.js bundle
  * zone.js
  * ...

## Build and existing infrastructure

### Webpack:
* include bundle in index.html
  * Reflect.js
  * Zone.js
  * bundle.js
    * application code
    * ...

+ build configuration

### What to use today
* SystemJS loader + Angular 2 bundles
* favorite tool you are most comfortable with

### Require vs. WebPack vs. JSPM
... open :)

### Future
* Webpack 2 coming
* Rollup
  * can create efficient bundles (i.e., containing only the used code)
* Angular2 CLI
* HTTP/2
