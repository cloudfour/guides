# Testing

## Philosophy
* Test code is a first-class part of the deliverable, not an optional nice-to-have.
* When scopeing / estimating work: always factor in testing. 
* Untestable code = bad code.
* Insufficent test coverage is better than no test coverage.
* Additional history and guiding principles are in [this "manitesto" doc](https://bitbucket.org/blog/save-time-with-default-pull-request-descriptions)

## Best Practices & Standardization

### General
* Organization of `scripts` in package.json:
	- `test` = runs all unit tests + E2E tests in headless mode
	- `test:watch` = same as `test` but with Jest in watch mode
	- `cypress` = run cypress with the dashboard open
	- `check-lint` = runs style lint, eslint, prettier
	- `lint` = same as `check-lint` but writes the changes (`--fix`)
	- `ci` = run EVERYTHING
* Try to minimize nesting and coupling. These make tests brittle and hard to maintain.

### Jest
* Unit test files for components should be siblings in the same directory with a `.test.js` suffix. Placing test code close to application code is intended to encourage testing and make it harder to forget.
* For the test name, prefer the `it('does something')` sytnax because it is more self-documenting and intuitive
* Use `describe()` and `beforeEach` sparingly. They lead to nesting and coupling.

### Testing Library
* Prefer the `getByRole` query over others because it typically best matches the user's experience. [1](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library#not-using-byrole-most-of-the-time)
* Avoid `getByTestId` because it _least_ matches the user's experience.
* We encourage using the `screen` object exported by Testing Library because the resulting idioms will be more similar in React and Vanilla JS projects. [1](https://testing-library.com/docs/queries/about#screen), [2](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library#not-using-screen).

## Favorite Tools
* Unit testing: Jest + Testing Library
* E2E testing: Cypress

## Resources
* [Common Testing Library mistakes](https://kentcdodds.com/blog/common-mistakes-with-react-testing-library)
* [Avoid Nesting](https://kentcdodds.com/blog/avoid-nesting-when-youre-testing)