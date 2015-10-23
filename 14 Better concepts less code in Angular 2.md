# Better concepts less code in Angular 2

## Slides


## Demo

* tabs
* tab-title & tab-content


## ng-content
Selects elements that match a css selector (== Transclusion concept of Angular 1).
Notation: `<ng-content select="child element of the component template"  />`

Example:

```
@Component({
    selector: 'app',
    template: `
        <tabs>
            <tab-title />
            <tab-content />
            <tab-title />
            <tab-content />
        </tabs>
    `
})
class App{  }


@Component({
    selector: 'tabs',
    template: `
        <div>
            <ng-content select="tab-title" />
        </div>

        <ng-content select="tab-content" />
    `
})
```

And the resulting code:

```
#document
<app>
    <div>
        <tab-title />
        <tab-title />
    </div>
    <tab-content />
</app>
```

## Get childrens
```
import {QueryList} from 'angular2/angular2';
...
class Tabs{
    @ContentChildren(TabTitle) // this allows us to get instances of children "TabTitle" components
    tabTitles: QueryList;

    nextTab();
}

...

@Component({
    selector: 'tab-title'
})
class TabTitle{
    show();
    hide();
    isVisible():boolean;
}
```

That way the Tabs component can get ahold of its children components.

## Content children

```
@Component({
    selector: 'app',
    template: `
        <my-widget>
            <comp-a />
        </my-widget>
    `
})
class App { ... }
```

`comp-a` is a _content child_: defined by the component's user. Content children are selectable with `ng-content`.

```
@Component({
    selector: 'my-widget',
    template: `
        <comp-b />
    `
})
class MyWidget { ... }
```

`comp-b` is a _view child_; it is a child that lives in the view of the component

## QueryList
QueryList is not an array but is similar to one. `QueryList` is iterable thus it can be used in a `for .. of` loop
It also has an observable property called `changes` which can be subscribed to in order to be notified whenever the content changes.

## Get children components
* @ContentChildren
* @ViewChildren

## TemplateRef
Allow to reference a chunk of UI
...

## Lifecycle
* OnChanges
* OnInit
* DoCheck
* OnDestroy
* AfterContentInit
* AfterContentChecked
* AfterViewInit
* AfterViewChecked
* ...


