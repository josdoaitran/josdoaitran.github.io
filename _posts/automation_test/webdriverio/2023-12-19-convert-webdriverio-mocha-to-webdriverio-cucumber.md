---
layout: post
title:  "How to convert a WebDriverio Mocha project to WebdriverIO Cucumber"
author: donald
categories: [ sharing, automation-test ]
image: assets/images/software-testing-general/software-testing-tools.jpg
---
Converting a WebDriverio Mocha project to WebdriverIO Cucumber

Refer to documents from WebdriverIO page, WebdriverIO supports us integrate our Automation testing framework with 3 frameworks:

- Mocha
- Jasmine
- **Cucumber**

At starting points of most of project, Automated testing framework projects will be created with Mocha. (Mocha is popular to adapt testing with Javascript and Typescript programing language.)

So we can receive the demands to convert the current project from Mocha testing framework to be enabled to integrate with Cucumber.

On this article, I would like to mention these steps to help us integrate WebDriverio with Cucumber.

**Install Cucumber and add cucumber in nodejs project**

Refer to the original documents from Webdriverio, we need to make sure Cucumber added in our testing project. we run this command on your project.

```bash
npm install @wdio/cucumber-framework --save-dev
```

Remove this row in package.json:

`"@wdio/mocha-framework": "^8.1.2",`

After that, the cucumber will be mentioned in package.json (Where we control all dependencies of our testing project.)

Basically, it can like here:

![walking]({{ site.baseurl }}/assets/images/automation-test/webdriverio-mocha-to-webdriverio-cucumber/Untitled.png)

Remove these files and folder: **node_modules** and **package-lock.json**

**Steps: Enable Cucumber in configuration file of Webdriveio project by Editing wdio.conf.js file**

+ **Edit value of framework field from mocha to cucumber:**

![walking]({{ site.baseurl }}/assets/images/automation-test/webdriverio-mocha-to-webdriverio-cucumber/Untitled 1.png)

it should be:

![walking]({{ site.baseurl }}/assets/images/automation-test/webdriverio-mocha-to-webdriverio-cucumber/Untitled 2.png)

**Update value of spec field:**

On mocha framework, we will configure where we input our test case as javascript files (.js)

```bash
specs: [
        './test/specs/**/*.js'
    ],
```

On WebdriverIO with Cucumber, we will configure where we input our test case as Feature file and following Gherkin language.

```bash
specs: [
        './features/**/*.feature'
    ],
```

For example, we will convert them like:

![walking]({{ site.baseurl }}/assets/images/automation-test/webdriverio-mocha-to-webdriverio-cucumber/Untitled 3.png)

**Update options of WebdriverIO from Mocha to Cucumber:**

On WebdriverIO with Mocha, we will have options field on wdio.conf.js file. We have to replace them by Cucumber options in WebdriverIO:

From:

```bash
// See the full list at http://mochajs.org/
    mochaOpts: {
        ui: 'bdd',
        timeout: 60000
    },
```

To:

```bash
// If you are using Cucumber you need to specify the location of your step definitions.
    cucumberOpts: {
        // <string[]> (file/dir) require files before executing features
        require: ['./features/step-definitions/**.js'],
        // <boolean> show full backtrace for errors
        backtrace: false,
        // <string[]> ("extension:module") require files with the given EXTENSION after requiring MODULE (repeatable)
        requireModule: [],
        // <boolean> invoke formatters without executing steps
        dryRun: false,
        // <boolean> abort the run on first failure
        failFast: false,
        // <boolean> hide step definition snippets for pending steps
        snippets: true,
        // <boolean> hide source uris
        source: true,
        // <boolean> fail if there are any undefined or pending steps
        strict: false,
        // <string> (expression) only execute the features or scenarios with tags matching the expression
        tagExpression: '',
        // <number> timeout for step definitions
        timeout: 60000,
        // <boolean> Enable this config to treat undefined definitions as warnings.
        ignoreUndefinedDefinitions: false
    },
```

**+ Update hook configuration of WebdriverIO from Mocha to Cucumber:**

From Mocha:

```bash
/**
     * Hook that gets executed before the suite starts
     * @param {Object} suite suite details
     */
    // beforeSuite: function (suite) {
    // },
    /**
     * Function to be executed before a test (in Mocha/Jasmine) starts.
     */
    // beforeTest: function (test, context) {
    // },
    /**
     * Hook that gets executed _before_ a hook within the suite starts (e.g. runs before calling
     * beforeEach in Mocha)
     */
    // beforeHook: function (test, context) {
    // },
    /**
     * Hook that gets executed _after_ a hook within the suite starts (e.g. runs after calling
     * afterEach in Mocha)
     */
    // afterHook: function (test, context, { error, result, duration, passed, retries }) {
    // },
    /**
     * Function to be executed after a test (in Mocha/Jasmine only)
     * @param {Object}  test             test object
     * @param {Object}  context          scope object the test was executed with
     * @param {Error}   result.error     error object in case the test fails, otherwise `undefined`
     * @param {Any}     result.result    return object of test function
     * @param {Number}  result.duration  duration of test
     * @param {Boolean} result.passed    true if test has passed, otherwise false
     * @param {Object}  result.retries   informations to spec related retries, e.g. `{ attempts: 0, limit: 0 }`
     */
    afterTest: async function(test, context, { error, result, duration, passed, retries }) {
        if(error){
            await browser.takeScreenshot();
        }
    },

    /**
     * Hook that gets executed after the suite has ended
     * @param {Object} suite suite details
     */
    // afterSuite: function (suite) {
    // },
```

 To Cucumber

```jsx
/**
     * Cucumber Hooks
     *
     * Runs before a Cucumber Feature.
     * @param {String}                   uri      path to feature file
     * @param {GherkinDocument.IFeature} feature  Cucumber feature object
     */
    // beforeFeature: function (uri, feature) {
    // },
    /**
     *
     * Runs before a Cucumber Scenario.
     * @param {ITestCaseHookParameter} world    world object containing information on pickle and test step
     * @param {Object}                 context  Cucumber World object
     */
    // beforeScenario: function (world, context) {
    // },
    /**
     *
     * Runs before a Cucumber Step.
     * @param {Pickle.IPickleStep} step     step data
     * @param {IPickle}            scenario scenario pickle
     * @param {Object}             context  Cucumber World object
     */
    // beforeStep: function (step, scenario, context) {
    // },
    /**
     *
     * Runs after a Cucumber Step.
     * @param {Pickle.IPickleStep} step             step data
     * @param {IPickle}            scenario         scenario pickle
     * @param {Object}             result           results object containing scenario results
     * @param {boolean}            result.passed    true if scenario has passed
     * @param {string}             result.error     error stack if scenario failed
     * @param {number}             result.duration  duration of scenario in milliseconds
     * @param {Object}             context          Cucumber World object
     */
    // afterStep: function (step, scenario, result, context) {
    // },
    /**
     *
     * Runs after a Cucumber Scenario.
     * @param {ITestCaseHookParameter} world            world object containing information on pickle and test step
     * @param {Object}                 result           results object containing scenario results
     * @param {boolean}                result.passed    true if scenario has passed
     * @param {string}                 result.error     error stack if scenario failed
     * @param {number}                 result.duration  duration of scenario in milliseconds
     * @param {Object}                 context          Cucumber World object
     */
    // afterScenario: function (world, result, context) {
    // },
    /**
     *
     * Runs after a Cucumber Feature.
     * @param {String}                   uri      path to feature file
     * @param {GherkinDocument.IFeature} feature  Cucumber feature object
     */
    // afterFeature: function (uri, feature) {
    // },
```

**- Steps: Create features, step-definitions folder and step-definitions class**

![walking]({{ site.baseurl }}/assets/images/automation-test/webdriverio-mocha-to-webdriverio-cucumber/Untitled 4.png)

## Step: Convert current Test Case to Feature file:

The original test case:

![walking]({{ site.baseurl }}/assets/images/automation-test/webdriverio-mocha-to-webdriverio-cucumber/Untitled 5.png)

Test case in Gherkin language and feature file:

![walking]({{ site.baseurl }}/assets/images/automation-test/webdriverio-mocha-to-webdriverio-cucumber/Untitled 6.png)

- **StepDefinition** Class: we will import `@wdio/cucumber-framework` and define the method to execute the actions as we implement in page object classes

```jsx
Given(/I access to (\w+) page$/, async (page) =>{
    await LoginPage.open(page)
});

When(/I input my username (\w+) and passsword (.+)$/, async(username, password) => {
    await LoginPage.login(username, password)
});

Then(/I can see the flash messsage with content (.*)$/, async (messsage) => {
    await expect(SecurePage.flashAlert).toBeExisting();
    await expect(SecurePage.flashAlert).toHaveTextContaining(messsage);
});
```

To implement stepDefinition methods, we based on **Regular-Expressions**: https://www.regular-expressions.info/

- Update Default export of Page class:

From

`module.exports = new LoginPage();`

To:

`export default new LoginPage();`

Then, in page class we will have this structure:

```jsx
/**
 * sub page containing specific selectors and methods for a specific page
 */
class LoginPage extends Page {
    /**
     * define selectors using getter methods
     */

    /**
     * a method to encapsule automation code to interact with the page
     */
    
}

export default new LoginPage();
```

- **Update package.json to be suitable with Javascript ES6 syntax** (To make sure our test script interact with our browser)

We need to update these dependencies on package.json.

```jsx
"@babel/cli": "^7.6.4",
"@babel/core": "^7.6.4",
"@babel/preset-env": "^7.6.3",
"@babel/register": "^7.6.2"
```

then, we run this command: npm install

and run test again.

if we still get troubles in executing test and interact with browser, we have to do 2 steps:

- update wdio.conf.js

```jsx
requireModule: [
            '@babel/register'
          ],
```

- create the file **babel.config.js** with context:

![walking]({{ site.baseurl }}/assets/images/automation-test/webdriverio-mocha-to-webdriverio-cucumber/Untitled 7.png)

```jsx
module.exports = {
    presets: [
      ['@babel/preset-env', {
        targets: {
          node: 12
        }
      }]
    ]
  }
```

                                   — Copyright 2024 — 