# Unit testing strategies for Angular 2

## General principles
* use the smallest tests possible
  * use a unit test if possible
* tests must be readable
* tests public interfaces, not private implementation details (those should be covered when testing the public API)
* don't mock unless there is a reason to
* test all the time
* make tests fail
