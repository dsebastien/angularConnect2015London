# Code Happy with TypeScript

## Tools can help you code happy
* automate time consuming tasks
* give you more confidence in the quality of what you create
* manage de level of complexity

## Time vs complexity
* version control quickly required
* then automated tests
* then code reviews

## TypeScript for Angular projects
* tools come with a cost, benefits and applicability
* TypeScript helps in the whole project lifespan
  * easy setup, benefit from the get go
  * incremental -- optional typing
  * flexible -- ES5 syntax ok
  * scalable

TS has a great cost/benefit ratio

## Why Angular loves TS
* renaming
* code navigation
* type checks
* linting/formatting
* build toolchain

## Source tooling
* Angular 1 built testing into the framework
* Angular 2 adds static types to the framework

Now they work on making TS with Angular easy for us.

## Demo
Quick project init:

```
npm install typescript angular2
./node_modules/.bin/tsc --init --target es5 --experimentalDecorators --emitDecoratorMetadata
```

* Gulp
  * They use Gulp on TypeScript (among other things).
  * They use it to build the code, watch everything, etc.
* Sourcemaps
  * They use sourcemaps to easily navigate to original TS code, debug in it
* Separate build output from sources












