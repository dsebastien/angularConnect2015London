# Iterative version upgrade strategies for large applications

## Writing upgradeable code
* use public APIs
  * avoid private ($$) properties
  * be suspicious of undocumented behavior
  * if you can't
    * write thorough tests
    * write abstraction layers
    * talk to the community

## Write abstraction layers
* code duplication increases to upgrade
* common code allows adopting new features

## Test types
Automation is key to success.

* compilation tests: TypeScript is great for this
* unit tests: Jasmine & Karma
* integration tests: Protractor
* screenshot tests

## Ensuring coverage
* unit tests: Karma-coverage
* integration tests: what does this mean?
  * they log the pages touches by the integration tests
  * then compare that to the analytics (which urls the users actually hit))
* easily missed areas
  * conditional states
  * error handling

## Version upgrades
Minor ones:
* update library locally
* run all test suites
* if problems are found: fix those one by one and commit those fixes one by one
* re-run all test suites (iteratively)
* release!
* adopt new features

## Iterative migration strategy
* include new major library or version
* iteratively update existing features
* examples: Angular 2, Component Router, TypeScript


