# Testing

## Philosophy
* Test code is a first-class part of the deliverable, not an optional nice-to-have.
* When scoping / estimating work: always factor in testing. 
* Testability is an attribute of good code. Code that cannot be tested is a problem.
* Insufficient test coverage is better than no test coverage.
* Prefer [Use Case Coverage over Code Coverage](https://kentcdodds.com/blog/how-to-know-what-to-test) (no need for 100% code coverage).
* Additional history and guiding principles are in [this "manifesto" doc](https://docs.google.com/document/d/1XWx0GZLndtPF4-cwBeHii85osRj0ROPrflBF3DAVewA/edit)

## Best Practices & Standardization

### General
* Organization of testing scripts in `package.json` ([more details](../package-json-script-names.md))
  * `npm run test`: Runs all test runners (Jest and/or Cypress)
  * `npm run test:watch`: Runs all test runners in watch mode
  * `npm run test:jest`: Runs Jest and exits
  * `npm run test:jest:watch`: Runs Jest in watch mode
  * `npm run test:cypress`: Runs Cypress and exits
  * `npm run test:cypress:open`: Open Cypress dashboard

* [Apply the AHA principle](https://kentcdodds.com/blog/avoid-nesting-when-youre-testing). Try to minimize nesting, coupling and over-abstraction. These make tests brittle and hard to maintain.

### Jest
* Unit test files for components should be siblings in the same directory with a `.test.js` suffix. Placing test code close to application code is intended to encourage testing and make it harder to forget.
* For the test name, prefer the `it('should do something')` syntax because it is more self-documenting and intuitive
* Use `describe()` and `beforeEach` sparingly. They lead to nesting and coupling.

### Testing Library
* Prefer the `getByRole` query over others because it typically best matches the user's experience. [1](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library#not-using-byrole-most-of-the-time)
* Avoid `getByTestId` because it _least_ matches the user's experience.
* We encourage using the `screen` object exported by Testing Library because the resulting idioms will be more similar in React and Vanilla JS projects. [1](https://testing-library.com/docs/queries/about#screen), [2](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library#not-using-screen).

## Favorite Tools
* Unit/integration testing: Jest + Testing Library
* E2E testing: Cypress

## Resources
* [Common Testing Library mistakes](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library)
* [Avoid Nesting](https://kentcdodds.com/blog/avoid-nesting-when-youre-testing)
