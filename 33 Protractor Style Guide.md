# Protractor style guide

## E2E Testing
Testing the entire application that connects to a middle tier, ...

Why is E2E important?
* Tells you that everything is working as expected
* Prevents production incidents
* Manual testing takes too much time

What does E2E test?
* major subpages or routes in the application
* main user interaction flows
* essential elements on a page

## Styleguide
* generic rules
* project structure
* locator strategies
* page objects
* test suites

## Generic rules - Do not e2e test what's been unit tested
* unit tests are much faster than e2e tests
* avoid duplicate tests

## Generic rules - Use one configuration file
* use your build tool to set up different configurations
* avoid duplicate configuration code

Example:
```
e2e.local: {
    options: {
        args: {
            baseUrl: local_base_url,
            seleniumAddress: local_Se,
            specs: ['.../**/*.spec.js']
        }
    }
}

e2e.dev:
...
```

## Project structure
Group e2e tests in a structure that makes sense to the structure of your project:
* easy to find
* separates them from unit tests
* cleaner folder structure

Avoid:
```
* app\home
  * home.module.js
  * home.controller.js
  * home.controller.spec.js
  * home.e2e.spec.js
  * home.page.js
* ...
```

Recommended:
```
* app\home
  * home.module.js
  * home.controller.js
* app\profile
  * profile.module.js
  * profile.controller.js
  * profile.directive.js
* test
  * e2e
    * home
      * home.page.js
      * home.spec.js
    * ...
```

## Locator strategies
NEVER use xpath:
* markup is very easily subject to change
* xpath has performance issues
* unreadable locator

Prefer by.id and by.css when no protractor locators are available:
* access elements easier
* select markup that is less likely to change
* more readable locators

By.id is very efficient

Avoid text locators for text that changes frequently
* text for buttons, links and labels tends to change over time
* tests should not break when you make minor text changes

## Page Objects
Use page Objects to interact with the page under test
* encapsulate information about the elements on the page under test
* can be reused across multiple tests
* decouple the test logic from implementation details

Recommended:
```
var QuestionPage = require('./question.page');

describe('Question page', function(){
    var question = new QuestionPage();

    it('should ask any question', function(){
        question.ask('What is the purpose of meaning');
        expect(question.answer.getText()).toEqual('Chocolate');
    });
});
```

Question page:
```
var QuestionPage = function(){
    this.question = element(by.model('question.text'));
    this.answer = element(by.binding('answer'));
    this.button = element(by.className('question-button'));

    this.ask = function(question){
        this.question.sendKeys(question)-;
        this.button.click();
    };
};
module.exports = QuestionPage;
```

In addition:
* declare one page object per file
* have a single module.exports statement at the end
* require and instanciate all dependencies at the top
  * clearly show the dependencies

Example:
```
var UserPage = require('./user.page');
var MenuPage = require('./menu.page');

describe('User page', function(){
    var user = new UserPage();
    var menu = new MenuPage();
    // specs
});
```

Expose all public elements in the constructor: the user page should have quick access to the available elements on a page

Example:

```
var userPage = require('./user.page');

describe('User page', function(){
    var user = new UserPage();

    it('should work'), function(){
        user.name.sendKeys('bla');
        expect(user.saveButton.isEnabled()).toBe(true);
    }});
```

Don't make assertions in the page objects: that is the responsibility of the test. The reader should be able to understand the behavior of the application by looking at the test only.

Add wrappers for directives, dialogs and common elements:
* reuse those in multiple tests
* only one place to modify

Page objects should represent portions of the viewport, not necessarily a complete page.

## Test suites

### Don't mock unless you need to
Using the real application with all the dependencies gives you high confidence.
Mock when you cannot call the real application.

### Use Jasmine 2
* Jasmine 2 is well documented
* Supported by Protractor out of the box
* Supports beforeAll, afterAll, ...

### Make tests independent at file level
Allows to run tests in parallel using sharding.

The execution order is not guaranteed (which is why they should be independent).

You can run suites in isolation.

### Make tests independent from each other
Allows tests to run in isolation.

Allows to debug tests more easily.

Exception:
If operations performed to initialize the state of the test are too expensive.

### Navigate to the page under test before each test
Ensures that the page under test is in a clean state.

### Navigation suite
Have a test suite that navigates through the major routes of the application.

Makes sure that major parts of the application are correctly connected to each other.

Users usually don't navigate by manually entering URLs.

Gives confidence about permissions.


