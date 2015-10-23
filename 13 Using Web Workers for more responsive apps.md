# Using Web Workers for more responsive apps

## Links
* http://bit.ly/custom-message-bus
* bit.ly/web_worker_starter_pack

## Single process single threaded model
Too easy to block the UI / skip frames & be unresponsive to users

## 60 FPS
Means 16ms max to render a frame

~8ms needed for DOM updates

Many CPU/memory intensive operations

## WebWorkers
Benefits:
* application logic doesn't block the render thread
* run application across multiple windows or frames
* better compete performance-wise with native mobile apps
* test without the browser
* works with all modern browsers (IE 10+)
* more battery efficient

## Alternative
Do the work on the server side:
* if the data is on the device it doesn't make sense
* resources cost vs data plan usage costs

## Numbers everyone should know
* L1 cache reference
* branch mispredict
* ...

## Challenges
* no DOM access
* no shared memory (message passing)
* serialization
* concurrency issues

## Angular support
Run everything in a WebWorker let Angular manage the UI.

* load the angular2/bundles/web_worker/ui.dev.js
  * web worker

```
import {bootstrap} from "angular2/web_worker/ui";
...
```

Schema...

## Web worker compatible components
* full access to angular APIs
* no DOM access
* should use data bindings instead of manipulating the DOM
* can inject Renderer to programmatically alter DOM elements
* subset of regular Angular 2 components

## Custom elements
* create a custom element to run UI side code
* use lifecycle callbacks
* communicate back with Angular using DOM events
* limited to standard DOM events
* ...

## MessageBus
* language agnostic API for communicating with Angular components across any runtime boundary
* supports multiplet
* all messages must be serializable
* Analog to a MessageQueue

MessageBus between UI and worker

## MessageBroker
Used when want to execute code on the opposite side (ui -> worker or worker -> ui)

* application -> registerMethod(m) -> ServiceMessageBroker
* function m ...
* ...

## Custom MessageBus

Demo:
* one instance of an angular app
* use WebSocket to push data to all connected clients
