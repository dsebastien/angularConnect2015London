# Extreme programming in a nutshell

## Links
* slides: http://www.slideshare.net/RachelDavies/angularconnect-extreme-programming-in-a-nutshell-with-vikki

## Pair programming
Recommended to do it much more than for resolving specific problems during development.

Taken to the extreme: "mob programming", which is the idea to regroup 3-4 persons in a room and develop software one after another.

Also, pair programming supposedly greatly reduces the value of formal code reviews.

## Spikes
Done in solo to explore something. Code is thrown away afterwards.

## Test first
Give confidence in code. Avoid manual mistakes. Create acceptance test first. Helps focus on implementation. Makes sure that we build what is needed.

Helps to implement continuous delivery.

## Continuous delivery
Deploy several times a day. From implementation to live in a couple of hours.
The goal is to keep the development pipeline as short as can be and limit the number of barriers between a developer and deployment of code up to production.

To help with detecting issues, use extensive monitoring and measure various metrics (e.g., actual response times, CPU usage, memory usage, ...).

Use feature toggles to decouple releases from development. Features are enabled based on environment configuration. Once something is production ready, it is turned on in production.
