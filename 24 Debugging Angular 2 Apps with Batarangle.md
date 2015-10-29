# Debugging Angular 2 Apps with Batarangle

## Links
* https://github.com/rangle/batarangle
* http://rangle.io/batarangle

## Batarangle
Browser plugin that helps debugging Angular 2 applications.
Adds an 'Angular 2' tab in the developer tools.

Allows to visualize the Angular 2 application's component tree.
We can click on any component and get all the information about it.

## Future plans
* pushing bootstrap logic into Angular
* wrapping up tree view / component inspector
* showing updates: visually show when things get updated
* snapshots

## Under the hood
* watch the DOM, check for changes
* when changes are detected, they get the element and invoke an Angular 2 function to get the component
* currently tied to Google Chrome's Dev Tools API
