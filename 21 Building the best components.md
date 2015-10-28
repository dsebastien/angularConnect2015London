# Building the best components

## What makes a good component
* simple, straightforward APIs
* works consistently, reliably and performantly in all environments
* fully accessible for users of all abilities
* internationalized for users around the world
* documentation for general use and public API
* comprehensive demos
* robust unit tests, some e2e tests
* performance is measured and tracked

## Aspects to consider
* your component from the outside: how developers and users interact with your component
* your component from the inside

## Component on the outside

### Public API
Huge importance: public API

* component class (analogous to the controller in Angular 1)
* much more expressive in Angular 2
  * template syntax
  * @ContentChildren
  * @Host

Events fired by the component are also part of the public API
* given how change detection works in Angular 2, events will be used a lot more
* @Output also make it clear which events can be fired, compared with Angular 1 where any arbitrary string could be used as an event

### Accessibility
Ensure that a maximal number of users can use the component.

First, always use the right component for the job (e.g., prefer a real button over a div with a click event)

Second, bind aria attributes. For example: `<div class="cool-checkbox" role="checkbox" [attr.aria-checked]="isChecked">...</div>`

Other example:
```
@Component({
    selector: 'cool-checkbox',
    host: {
        'attr.role': 'checkbox',
        '[attr.aria-checked]': 'isChecked'
class CoolCheckbox { ... }
}
})
```

Make sure to support keyboard interaction for disabled users.
Angular 2 makes this very easy:

```
<div role="checkbox" class="zz-checkbox"
    (keydown.space)="toggle()"
    (keydown.u)="navigate()"
    (keydown.control.enter)="submit()"
    (keydown.alt.shift.escape)="superExit()"
    [attr.aria-checked]="isChecked"
    [attr.aria-disabled]="isDisabled"
```

Manage the focus correctly. For example if a popup is displayed, focus should remain in the popup even if the user hits tab multiple times:

```
<div tabindex="0" (focus)="myDialog.focus()"></div>
```

### Provide fakes
* provide those with your actual components
* expose a real API plus extra testing methods
* no real work, only tracks state
* can help hammer out the API
* makes testing more pleasant downstream

Example:
CoolComponent that uses a CoolDropDown component. For testing, it might be useful to use a fake CoolDropDown:

```
@Component({
    selector: 'cool-dropdown',
    template: ''
})
class FakeCoolDropDown implements CoolDropDown{
    // doesn't do much
}
```

Angular 2 provides a `testComponentBuilder`:

```
testComponentBuilder
    .overrideDirective(CoolComponent, FakeCoolDropDown)
    .createAsync(CoolComponentTest).then();
```

### Embrace Dependency Injection
...
* more testable
* looser coupling

Plus in Angular 2:
* scope explicitly to a component's content or view children
* can override injectable for a subset of the app

### Embrace the template
* concise, declarative syntax is better than ever
* direct DOM manipulation can get unorganized and hard to follow
* performance improvements for NG2 makes direct DOM much less necessary
* avoiding direct DOM manipulations enables
  * server-side rendering
  * running in a Web Worker

### Embracing types
* can find mistakes in code statically
* better tooling
* much easier to express function APIs
* generally makes code easier to understand

### Testing
Angular 2 provides the TestComponentBuilder:

```
beforeEach(inject([TestComponentBuilder], (tcb) => {
    builder = tcb;
}));

it('should test something', (done) => {
    builder.createAsync(TestApp).then(rootTestCmp => { ... });
});
```
