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
    })
})
```
