# Angular 2 Data Flow

## Links
* slides: g.co/ng/ac-dataflow
* Tactical: github.com/angular/tactical

## Event Streams
Take user inputs
* clicks
* drags
* inputs
* ...

Transform them:
* filtering
* mapping
* fetching

And generate some output:
* rendering
* templates
* change detection

## Goals
Think less:
* reasonable
* event flow

Prevent bugs:
* making the applications more predictable
* centralize state
* containment

Have a minimal runtime overhead

## Observables
Used throughout the Angular 2 codebase. Comes from the RxJS library created by Microsoft and available in many different languages (e.g., Java, Scala, .NET, ...).

Idea of "collection over time".

Facts:
* Observables are like Arrays
* Observables are like Promises but more powerful
* Observables are goind to be standardized as part of ES2016
* RxJS has hundreds of contributors
* RxJS has tons of utility methods that can manipulate the collection

## Autocomplete example (Typeahead)
An autocomplete can be implemented as follows using Angular 2:

```
// Template
<input type="text"
    [(ng-model)]="searchText"
    (keyup)="searchChanged($event)"
>

// Component
doSearch(){
    ...
    let searchText = this.searchText;

    this.currentRequest = fetch(`/stocks?symbol=${searchText}`)
        .then(res => res.json())
        .then(tickers => this.tickers = tickers);
}

searchChanged(){
    this.doSearch(this.searchText);
}

```

Problems with this approach:
* it isn't easy to implement throttling
* it isn't easy to cancel requests
* what if two requests are sent and the responses come in the wrong order or not at all?

In brief:
* out-of-band logic issues
* side effects
* more complexity

## Streams
Same example but with Observables and streams.

First, know that forms are observable
```
// Template
<input type="text"
    #symbol
    [ng-form-control]="searchText" // bind this input to the Control input on the controller
    placeholder="ticker symbol"

// Component
export class TypeAhead{
    searchText = new Control();

    constructor(){
        this.searchText.valueChanges // the Control object has a 'valueChanges' property which is an Observable of the valueChanges event on that component
            .debounceTime(200) // wait at least 200ms before emitting values

            .subscribe(...); // the subscription will receive events every time a character is typed in the input
    }
}
...
```

## Http
Http also implements Observable

```
load(val: string): Observable<any[]> {
    return this._http
        .request(`/stocks?symbol=${val}`)
        .map(res => res.json());
}
```

## switchMap
The two examples above can be combined to make something more interesting.
The switchMap RxJS operators does two things:
* take the input value and flatten it out: allows to treat the values as if those were synchronous (i.e., waits for the asynchronousness to resolve)
* if another response comes down the pipe while switchMap is flattening, then it will cancel the previous request

```
this.searchText.valuesChanges
    .debounceTime(200)
    .switchMap(val => ticketLoader.load(val))
    .subscribe(...);
```

## Pipes
Can accept async values and subscribe to an observable and wait for them to emit values.

Example:`{{ today | async | date }}`

Code:
```
// Template
The current date is: {{today || async || date}}

// Component
export Class Today{
    today: Promise<Date>;
    constructor(ts: TimeService){
        this.today = ts.getServerDate();
    }
}
```

To continue with the previous example, a first solution to bind the results to the view could be to do the following in the template:

```
<li *ng-for="#tick of tickers"> ... </li>
```

Another possibility is to use the AsyncPipe:

```
// Template
<li *ng-for="#tick of tickers | async"> ... </li>

// Component
this.tickers = this.searchText.valueChanges
    .debounceTime(200)
    .switchMap(val => {
        return tickerLoader.load(val);
        }
    );
```

The AsyncPipe will take care of the subscription, will get the result, return it then cancel the subscription.

## Angular Data Roadmap
### Goals
* reduce boilerplate
* improve testability
* enable high performance

### Template transforms
* plugin to transform Angular templates
* runs during compilation, on application load

Example:
```
// developer writes
<div>
    {{model.firstName}}
    {{model.lastName}}
</div>

// a transformer can generate
<div>
    {{model.get("firstName")}}
    {{model.get("lastName")}}
</div>
```

For app devs:
* better sugar for third party libraries
* create DSLs in templates
* optimize queries with view metadata

Transformers work on the AST used by the Angular compiler and the transformer produces a new tree


### Tactical
Data access library. Outside of Angular core.

Offline first approach:
* works against most APIs
  * focus on user experience
    * cache reads
    * eventual consistency for writes
    * client-side conflict resolution

Tactical uses observables:
* freshest available
* offline mutations with background sync
* first write wins guarantee
* server-side push if back-end supports it

Edge cases:
* List vs Get request
* Arbitrary searches
* Prefetching

Tactics:
* applications can integrate logic to extend the Tactical model
* add context to improve UX
  * ...

Current state:
* in development
* offline reads/writes

