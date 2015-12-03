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
module.expoerts = QuestionPage;
```
