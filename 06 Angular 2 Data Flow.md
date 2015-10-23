# Angular 2 Data Flow

## Links
* slides: g.co/ng/ac-dataflow
* Tactical: github.com/angular/tactical

## Event Streams
User inputs
* clicks
* drags
* inputs
* ...

Transforms:
* filtering
* mapping
* fetching

Think less:
* reasonable
* event flow

Prevent bugs
* state
* containment

## Forms
Forms are observable
```
<input type="text" #symbol [ng-form-control]="searchText"
...
```


## switchMap
...

## Pipes
Can accept async values and subscribe to an observable and wait for them to emit values.

Example:`{{ today | async | data }}`

## Angular Data Roadmap
### Goals
* reduce boilerplate
* improve testability
* enable high performance

### Template transforms
* plugin to transform Angular templates
* happens during compilation, on application load

For app devs:
* better sugar for third party libraries
* create DSLs in templates
* optimize queries with view metadata

Transformers work on the AST used by the Angular compiler and the transformer produces a new tree


### Tactical
Offline first approach:
* works against most APIs
* * focus on user experience

Tactical uses observables:
* freshest available
* offline mutations with background sync
* first write wins guarantee
* ...
...

Edge cases:
* List vs Get request
* Arbitrary searches
* Prefetching

Tactics:
* application extensions to the model
* add context to improve UX
  * ...

Current state:
* in development
* offline reads/writes

