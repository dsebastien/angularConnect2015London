# How to design large AngularJS applications that scale

## About
Goal: design in a way that permit applications to scale and to remain maintainable.

## Components
Components take inputs and outputs. They have clearly defined boundaries.

But what about real world applications? Large applications often have large component trees and design questions arise:
* how to share functionality
* how to give components context

All logic goes upwards.

* Controller
  * MessageList
    * MessageItem
      * DeleteButton

## Approaches to improve the code
* create small UI building blocks that can be reused and placed anywhere
* separate UI components and business logic

SRP remains of paramount importance.

## Smart and dumb components

### Dumb component
* only UI and View-specific actions
* bound inputs and bound outputs
* keeps and mutates its internal state
* no knowledge of the outside world
* no interaction with services
* receives context and callbacks via bindings

### Smart component
* wraps one or more dumb components
* connects them with the business layer. This is done by providing context to the dumb components.
* provides callbacks for dumb components

## Universal data flow system
Inspired by the Flux pattern pushed by Facebook.

A state layer is responsible to hold the application state and trigger change events.

The action layer is the core of the application.

Options for the state layer:
* several store-like custom services
* single store (reducer pattern?)
* router?
* reactive streams

State -> Smart(Dumb) components -> Actions -> * -> State

## Concepts
* state layer: holds application state, fires change notifications
* smart components: wires business and view layers together, provides context to dumb components
* take inputs and outputs, UI, pure and highly reusable
* actions: bundle side effects, triggers state changes

Unidirectional data flows makes it easy to separate concerns. Combining the two gives you a clean predictable architecture that scales.
