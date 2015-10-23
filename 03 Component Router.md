# Component router

## Intro
...

## Config

Path part of the route config:
* '/' - matches '/' or ...
* ...

Router params:
...

## Creating links
* 'as' property: name for the route
* router-link directive
  * / -> absolute
  * name: corresponds to the 'as'
  * generates an `<a href...`

## Child routes
`{ path: '/email/:id/...'}`

The '...' are needed to denote that the component has child routes.

...

To link to a child component:
...

## Eleven dimensional routing
...

## Conclusion
* few simple parts: RouterConfig, RouterOutlot and RouterLink
* child and auxiliary routes fully compose -- you can nest child routes inside auxiliary routes...
* ...
