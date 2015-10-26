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

`comp-b` is a _view child_; it is a child that lives in the view of the component.

When angular instanciates a component, it takes a component, clones it and the result of instanciating the template is called a View.

## QueryList
QueryList is not an array but is similar to one. `QueryList` is iterable thus it can be used in a `for .. of` loop.

It also has an observable property called `changes` which can be subscribed to in order to be notified whenever the content changes.

## Get children components
* @ContentChildren: get children that a user would put in a component when he uses it
* @ContentChild
* @ViewChildren: children placed in the template by the component's developer
* @ViewChild

## TemplateRef
Allow to reference a chunk of UI

```
@Component({
    selector: 'conf-talks',
    template: `
        <ul>
            <template ng-for [ng-for-of]="talks" [ng-for-template]="itemTemplate" />
        </ul>
    `
})
class ConfTalks{
    @Input() talks;
    @ContentChild(TemplateRef) itemTemplate;

    ...
}
```

In the example above, we get the template reference using `@ContentChild(TemplateRef)` and we use template ng-for to render it multiple times.

## Lifecycle
* Component Element
  * OnChanges
  * OnInit
  * DoCheck
  * OnDestroy
* Content Children
  * AfterContentInit
  * AfterContentChecked
* View Children
  * AfterViewInit
  * AfterViewChecked
* ...

## Form and input

```
@Component({
    selector: 'cont-talks',
    template: `
        <form>
            Speaker: <input ng-control="speaker" minlength="3">
        </form>
    `
})
class ConfTalks{
    ...

    @Input() set talks {
        this._talks = talks;
        this.filteredTalks = talks;
    }

    @ViewChild(NgForm) form; // will be populated after the View has been created (i.e., after the template has been loaded)
    ...

    afterViewInit(){
        let changes = this.form.control.valueChanges; // observable
        changes
            .filter(_ => this.form.valid) // only emit values when the input is valid
            .throttle(500) // only emit values after 500ms of inactivity
            .subscribe(value => this.filterTalks(value)); // subscribe

        ...
    }

    filterTalks(filters){
        this.filteredTalks  = this._talks.filter(
            t => t.speaker.indexOf(filter.speaker) > -1);
    }
}
```

