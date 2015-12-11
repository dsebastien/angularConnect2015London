# Turn the performance knob to 11

## AngularJS performance tips
* updrade Angular version regularly (many performance improvements)
* minimize the number of watchers
* use "track by"
  * if you change the order in a list you don't want to recreate the DOM and "track by" can help
* precompute filter expressions
* limit DOM to visible elements
* do not run digest all the time
* do not run digest after each HTTP request ($http.useApplyAsync(true))

## How to approach performance optimization
Don't optimize prematurely.

