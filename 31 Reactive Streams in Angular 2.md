# Reactive Streams in Angular 2

## Links
* RxJS Next: https://github.com/ReactiveX/RxJS

## RxJS 5
Goals:
* performance
* improved debugging
* ES7 observable spec alignment

## Performance
* decisions guided by performance tests
* tried multiple architectures
* > 120 micro performance tests
* ~10 macro performance tests using Angular's Benchpress
* operators ~4x faster

## Debugging
Improved experience

## Beta
Around the corner

## Reactive programming
* treat events as collections
* manipulate these sets of events with operators

## Angular 2
Angular 2 uses RxJS 5 Observables rather than promises

## Promises
* read-only view to a single future value
* success and error semantics via .then()
* not lazy: by the time you have a promise, it's on its way to being resolved
* immutable and uncancellable. Your promise WILL resolve or reject, and only once

## Observables
* "Streams" or sets
  * 0-n things
  * over any amount of time
* lazy: Observables will not generate values via an underlying producer unless they're subscribe to
* can be unsubscribed from
  * the underlying producer can be told to stop and even tear down

## Promises and Observables
Were both made to avoid callback hell.

## Types of async in modern Web applications
* DOM events (0-n values)
* animations (cancellable)
* AJAX (1 value)
* WebSockets (0-n values)
* server-sent events (SSE) (0-n values)
* alternative inputs (voice, joystick, ...) (0-n values)

## Promises are good for
* really only AJAX
  * or almost

SPAs commonly prepare data for a view via AJAX.
When the view changes, the next view probably doesn't care about the previous data.

Fortunately XHRs can be aborted!

... but promise-based AJAX libraries cannot be aborted, because promises can't be cancelled!

## Going from Promises to Observables
Using an Observable:
```
let subscription = x.subscribe(valueFn, errorFn, completeFn);

...
subscription.unsubscribe();
```

Creating an Observable:
```
let o = new Observable(observer => {
    const token = doAsyncThing((err, value) => {
        if(err){
            observer.error(err);
        }else{
            observer.next(value);
            observer.complete();
        }
    });

    // the returned function below will be invoked when unsubscribe is called
    return () => {
        cancelAsyncThing(token);
    };
});
```

Compared to creating a Promise:
```
let p = new Promise((resolve, reject) => {
    doAsyncThing((err, value) => {
        if(err){
            reject(err);
        }else{
            resolve(value);
        }
    });
});
```

## Helpers
* Observable.of(value, value2, ...)
* Observable.from(promise/iterable/observable)
* Observable.fromEvent(item, eventName)
* Angular's HTTP and Realtime Data services
* community-driven RxJS modules and libraries

## Error handling
Similar to promises:

```
myPromise.catch(error => {
    if(error instanceof OkayError){
        return Promise.resolve('okay');
    } else{
        throw error;
    }
});
```

With Observables:

```
myObservable.catch(error => {
    if(error instanceof OkayError){
        return Observable.of('okay');
    }else {
        throw error;
    }
});
```

Finally:

```
myPromise.finally(() => {
    console.log("done");
});
```

Observable code is exactly the same in this case.

Observables can be retried:

```
myObservable.retry(3);

myObservable.retryWhen(errors =>
    errors.delay(3000));
```

## Observable recap
* an observable is a set of any number of things over any amount of time
* all values are pushed to the nextHandler
* if there is an error, the errorHandler is called
* when completed, the completionHandler is called
* observables are lazy, they don't start producing values until subscribe() is called
* observables can be unsubscribed from

```
let sub = observable.subscribe(nextHandler, errorHandler, completionHandler);
sub.unsubscribe();
```

## Operators
Methods on observables that return observables.

Operators pass each value from one operator to the next, before proceeding with the next value in the set.

This is different from array operators (e.g., map and filter) which will process the entire array at each step.

That behavior can be changed using schedulers.

## Hot vs cold
Observables are cold by default.

* cold observables create a new producer each time a consumer subscribes to them
* hot observables share a single producer with every consumer that subscribes to them

## Warnings
* some operations can happen synchronously or asynchronously
* you can run into memory issues if you combine two observables (e.g., using the zip operator) and one produces value much faster than the second observable
