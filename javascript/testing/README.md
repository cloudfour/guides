<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Testing JavaScript](#testing-javascript)
  - [Overview](#overview)
    - [Why test?](#why-test)
    - [Costs and benefits](#costs-and-benefits)
    - [Building a practice of testing](#building-a-practice-of-testing)
  - [The language of tests](#the-language-of-tests)
    - [Examples](#examples)
  - [Types of tests](#types-of-tests)
    - [Unit](#unit)
    - [Integration](#integration)
    - [End-to-end](#end-to-end)
    - [Snapshot](#snapshot)
      - [Visual regression](#visual-regression)
  - [Test organization](#test-organization)
    - [Placement and naming of tests](#placement-and-naming-of-tests)
    - [Test blocks](#test-blocks)
    - [Setup and teardown](#setup-and-teardown)
    - [Test object factories](#test-object-factories)
  - [Tools](#tools)
    - [Runners](#runners)
    - [Assertion libraries](#assertion-libraries)
    - [Test doubles](#test-doubles)
      - [Fakes](#fakes)
      - [Stubs](#stubs)
      - [Mocks & Spying](#mocks--spying)
    - [Code coverage testers](#code-coverage-testers)
    - [Frameworks](#frameworks)
  - [Testable code](#testable-code)
    - [Functional style](#functional-style)
    - [Managing dependencies](#managing-dependencies)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Testing JavaScript

## Overview

WIP.

This guide is meant to be both a general reference and place for documenting team-specific standards and approaches. It will be JavaScript-specific, and focust on client-side testing, but many of the concepts discussed can apply to testing across languages and platforms.

### Why test?

Writing, maintaining, and automatically running tests for significant portions of in-house generated code is considered the best way to have confidence that software will perform according to requirements, over time. This practice also helps catch bugs during development and, depending on the workflow adopted, can also be used as a scaffold for writing the code itself (see test-driven development).

### Costs and benefits

In agency work, particularly, clients may need to be convinced of the benefits of testing, considering the time and effort needed to create, run, and maintain tests. In this light, the costs of testing can be weighed against the inevitable costs of shipping and fixing buggy software.

### Building a practice of testing

It also takes time to build developers' skills in writing both tests and testable code, and knowing how to set up and configure the tooling needed to scaffold and run tests throughout the development and release lifecycle. The hope is that this guide will be one resource to help minimize the costs of adopting a testing practice, in the hope that it becomes a standard practice on many, if not all projects.

<!---
(@TODO - Decide whether to keep the following reference)
-->

A decent overview of both general and JS-specific testing concepts and tools can be found in [this article](https://medium.com/welldone-software/an-overview-of-javascript-testing-in-2019-264e19514d0a) by Vitali Zaidman.

## The language of tests

Tests can be written in a few styles, with the language provided by what's known as an assertion library.

Most tests are written using `assert`-, `expect`-, or `should`-style assertion interfaces (see examples, below).

No matter what the style, a function, portion of code, or automted UI flow is run, and then the test executes a statement that must evaluate to true for the test to pass.

### Examples

```js
// Assert style
test('Two plus two equals four', () => {
  assert.equal(2 + 2, 4);
});
```

or

```js
// Expect style
test('Two plus two equals four', () => {
  expect(2 + 2).toEqual(4);
});
```

or

```js
// Should style
test('Two plus two equals four', () => {
  should(2 + 2).be.exactly(4);
});
```

These concepts can apply to almost any type of test. For example:

```js
// Run code that renders, compare with past snapshot
test('Nothing has changed', () => {
  expect(renderedOutput).toMatchSnapshot();
});
```

or (at a point in an integration or end-to-end test flow)

```js
// Automate a user login flow, then
test('User is logged in correctly', () => {
  expect(user.loggedIn).toBeTrue();
});
```

### Behavior-Driven Development (BDD)
The `should` assertion style, in particular, as well as the `expect` style, can be seen as aligned with the concept of behavior-driven development.

In short, both of these assertion styles allow natural-language like assertion statements. 
The `should` style takes this furthest, by optionally extending the object prototype. 
This allows tests to be written the way they might be by a project stakeholder:

```js
const customer = {
  loggedIn: false
};
const login = person => person.loggedIn = true;
// Automate a user login flow, then
test('Customer is logged in correctly', () => {
  customer.loggedIn.should.be.false;
  login(customer);
  customer.loggedIn.should.be.true;
});
```

## Types of tests

There are a handful of different, commonly recognized types of tests, each of which has a specific focus and purpose. Some should be run during development and as part of a VCS workflow, and others are meant to be run mainly in CI and deployment stages.

### Unit

Unit tests are designed to verify the functionality of the smallest building blocks of code. They are usually specced at the level of single functions or class methods. A suite of unit tests might cover most or all of the functions within a single (ES) module or the methods of a particular class.

Unit tests strive to isolate the subject of the test by using test doubles to predictably control the behavior of dependencies and eliminate side-effects. For example, a call to an API might be replaced with something like

```js
const apiCall = () => Promise.resolve({ data: { someKey: someValue } });
```

Test doubles can also be made to track details about their use (aka, act as `spies`), and testing libraries and frameworks generally supply methods that provide this functionality out of the box.

### Integration

Integration tests verify the correct coordination of functionality between modules or classes (both internal and possibly external [3rd-party]). Because integration tests are meant to verify the behavior of a system, fewer or maybe no units of code involved in the test may be substituted with test doubles.

### End-to-end

End-to-end (aka, E2E) tests verify expected outcomes of complete user flows by automating interaction with a running application. For web applications, this means spawning a fully built application in a real browser (may be headless) and having a test runner follow instructions to interact with (or drive) that browser through a user flow, simulating real-world use. In this scenario, nothing is faked, other than the user.

### Snapshot

Snapshot tests compare a portion of the current state of code or output (generally) in an application with a previous record of that same piece of state. In this way, a test can verify that something hasn't, or maybe has changed, and that this outcome was expected. If a code update results in a change where one wasn't expected (for example), the baseline can be reset for follow-up tests to use as a comparison.

#### Visual regression

## Test organization

### Placement and naming of tests

### Test blocks

### Setup and teardown

### Test object factories

## Tools

### Runners

### Assertion libraries

### Test doubles

[Reference](https://blog.pragmatists.com/test-doubles-fakes-mocks-and-stubs-1a7491dfa3da)

[Another reference](https://stackoverflow.com/questions/3459287/whats-the-difference-between-a-mock-stub#17810004)

(find more)

#### Fakes

#### Stubs

#### Mocks & Spying

### Code coverage testers

### Frameworks

## Testable code

### Functional style

### Managing dependencies
