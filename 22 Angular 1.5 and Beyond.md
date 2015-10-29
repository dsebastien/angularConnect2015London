# Angular 1.5 and Beyond

## Angular 1 versions
* v1.3 and 1.2 are just receiving security patches
* v1.4 is stable, receiving bug fixes
* v1.5 is in active development, receiving new features

## What's coming in Angular 1.5

### Simpler component definitions
```
mod.component('myComp', {
    template: '...',
    bindings: { ... },
    controller: function(){ ... }
})
```

### Multi slot transclusion

```
<pane>
    <pane-title>
        <a ng-click="...">a title</a>
    </pane-title>
    <pane-content>
        the content of the pane
    </pane-content>
</pane>
```

And the component:
```
mod.directive('pane', function(){
   return {
    restrict: 'E',
    transclude: {
        paneTitle: '?titleSlot',
        paneContent: 'contentSlot'
    },
    template: `
        <h1 ng-transclude="titleSlot"></h1>
        <div ng-transclude="contentSlot"></div>
    `
   }
});
```

### Better performance
* Lazy compilation
  * reduces bootstrap time by 25%
  * reduces initial memory pressure by 50%
  * resolves most recursive directive issues
* New $sanitize
  * reduces angular-sanitize.min.js zip by 3K

## Easing the upgrade to Angular 2

### Challenges for upgrading
* skill up your team in the languages and tools
* prepare the code for Angular 2
* benefit from modules and decorators
=> covered by ng-forward (https://github.com/ngUpgraders/ng-forward)

* use Angular 2 alongside Angular 1
* upgrade component by component
* benefit from Angular 2 performance
=> covered by ng-upgrade

Steps:
* prepare components for migration using ng-forward (make them closer syntactically to ng2)
* use ng-forward to move the prepared component to NG2
* once most of the app has been converted, remove ng-upgrade

Detailed steps:
* convert syntax using ng-forward
* upgrade components to ng2 using ng-forward+ng-upgrade
* remove ng-forward
* upgrade everything else to get a full Angular 2 app
