# Creating realtime apps with Angular 2 and Meteor

## Modern Web UIs
* modern UI
* no refresh
* more native-like Web apps
* used in the browser, on mobile, ...
* actual APPS

## Connected client-apps
* different type of architecture
* require a stateful server
* stateful apps on the client side
* push live updates from the server to the clients
* when a client pushes an update, it is saved instantly locally (i.e., no loading button -- they talk about optimistic UI) and synced with the server as soon as possible
* same experience on multiple platforms

## What is Meteor
Three concepts:
* open source framework using the connected client architecture
* embraces the idea of having JavaScript everywhere
* complete open platform

## Connected client
On the server side, Meteor provides:
* Livequery: like a watch on the database
  * query the DB constantly (efficiently) and check for changes
  * when changes are detected, all clients are notified directly
* ...

On the client side, Meteor provides
* Client Data Cache (Synced cache) (using Minimongo)
  * saves a lot of code for writing syncing code
* ...

## JavaScript everywhere
On both the back-end and front-end sides (aka isomorphic JavaScript)

With Metor, the API is the same on all layers

The power comes from combining the isomorphic aspect with the Meteor Data Flows
* WebSockets (for the realtime aspect and pub/sub)

## Complete Open Platform
* HTML templates
* App Logic
* Meteor
  * Reactive UI update system
  * Native mobile container
  * Speculative client-side updates
  * Client-side data store
  * Custom data sync protocol
  * Realtime database monitoring
  * Build & update system

+ Microservices & Database

## Comparison
Meteor can be compared to .NET & Java: it's a complete platform

## Stats
* Ranked 1st on GitHub's Web Application Frameworks
* Over 200 meetup groups
* Over 7000 community-authored packages

## Angular-Meteor
www.angular-meteor.com

## Angular2Now
Make it possible to use NG2 syntax on Angular 1

## Angular 2 and Meteor
There is an Angular 2 Meteor package: angular-meteor.com/angular2

* Smooth integration
* Regular Angular 2 syntax
* No need for Observables, Pipes
* Regular Meteor syntax


