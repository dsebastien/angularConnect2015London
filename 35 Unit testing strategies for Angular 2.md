# Unit testing strategies for Angular 2

## General principles
* use the smallest tests possible
  * use a unit test if possible
* tests must be readable
* tests public interfaces, not private implementation details (those should be covered when testing the public API)
* don't mock unless there is a reason to
* test all the time
* make tests fail

## Example usage of Angular 2 testing library
Subject to change (soon):

```
import {
    it,
    describe,
    expect,
    inject
} from "angular2/testing";
...

import {
    APP_ID
} from "angular2/angular2";

describe('default test injector', () => {
    it('should provide id', inject([APP_ID], (id) => {
        expect(id).toBe('abc');
    }));
});
```

Angular 2 provides wrappers for Jasmine (later also compatible with Mocha) which support dependency injection.

Another example:
```
import { it, ... } from "angular2/testing";
import { UserService"} from "../app/.../user-service";

describe('user service', () => {
    beforeEachProviders(() => [LoginService, UserService])

    it('should validate stuff', inject([UserService], (service => {
        service.stuff = 1234;
        expect(service.isValidStuff()).toBe(true);
    })));
});
```

## Async tests using injectAsync:

```
...
it('should validate stuff async', injectAsync([UserService], (service) => {
    service.stuff = 1234;

    return service.isValidStuffAsync().then((result) =>{
        expect(result).toBe(true);
    });
}), 3000); // timeout 3 sec
```

## Mocking

```
class MockingService extends LoginService{
    ...
}

describe('bla', () => {
    beforeEachProviders(() => {
        provide(LoginService, {useClass: MockingService}), UserService);
    });

    it('should greet', injectAsync([UserService], (service) => {
        return service.getGreeting().then((greeting) => {
            expect(greeting).toEqual('Welcome!');
        });
    });
})
```

Another option is the fakeAsync utility of Angular 2 testing.
fakeAsync wraps the entire test and it uses a zone to listen when setTimeout, setCallback... are registered. Instead of invoking them asynchronously, it will simulate moving time forward and invoke the functions immediately.

```
describe('with fake async', () => {
    beforeeachProviders(() => [LoginService, UserService]);

    it('should greet with fakeasync', inject([UserService], fakeAsync((service) => {
        var greeting;
        service.getGreeting().then(value) => {
            greeting = value;
        });

        tick(2000);

        expect(greeting).toEqual('Login failure!');

    })));
});
```

## Testing components
Angular 2 testing provides a TestComponentBuilder utility class.

The TestComponentBuilder always returns asynchronously, so always use injectAsync with it.

```
import {..., injectAsync, TestComponentBuilder, beforeEachProviders} from "angular2/testing";

describe('greeting component tests', () => {
    beforeEachProviders(() => {
        provide(LoginService, {useClass: MockLoginService}),
        UserService
    });

    it('should ask for PIN', injectAsync([TestComponentBuilder], (tcb) {
        return tcb.createAsync(GreetingComponent).then((fixture) => {
            fixture.detectChanges(); // you can detect changes on the fixture provided by TestComponentBuilder

            var compiled = fixture.debugElement.nativeElement;

            expect(compiled).toContainText("Enter PIN");
            expect(compiled.querySelector("h3")).toHaveText("Status: Enter PIN!!");

            // you can also modify the properties of the component directly:
            fixture.debugElement.componentInstance.greeting = "Foo";

            fixture.detectChanges(); // check if changes occurred
            // then check the native element again to see if the content has changed as expected
        });
    }));
});
```

RootTestComponent:
* test fixture returned by the TestComponentBuilder

```
class RootTestComponent {
    debugElement: DebugElement;
    abstract detectChanges(): void;
    abstract destroy(): void;
}
```

DebugElement:
```
class DebugElement {
    get componentInstance(): any;
    get nativeElement(): any;
    get elementRef(): ElementRef;
    get children(): DebugElement[];
    get componentViewChildren(): DebugElement[];
    query([By.css|By.directive]): DebugElement;
}
```

It's also possible to override values from the component to make it easier to test:

```
... injectAsync([TestComponentBuilder], (tcb) => {
        return tcb.overrideTemplate(GreetingComponent, `<span>{{greeting}}</span>`)
            .createAsync(GreetingComponent).then((fixture) => {
                ...
            });
    });
```

It's also easy to fire events:

```
...
    var compiled = fixture.debugElement.nativeElement;

    compiled.querySelector('button').click();

    return fixture.debugElement.componentInstance.pending.then(() => {
        fixture.detectChanges();
        expect(compiled.querySelector("h3")).toHaveText("Status...");"
    });
```

TestComponentBuilder allows to override many elements:
```
class TestComponentBuilder {
    overrideTemplate...
    overrideView...
    overrideDirective...
    overrideProviders...
    overrideViewProviders...
    createAsync...
}
```

## Tips
* Use `console.dump(obj);` to get all data contained in an object
* Use `ddescribe` to put focus on a specific describe block
* Use `iit` to put focus on a specific test
* Use `xit` to skip a test
* Use `xdescribe` to skip a describe
* Add `debugger;` anywhere in a test executed by Karma to have to stop at that point
  * in Chrome, it stops execution thus it's easy to inspect the variables
