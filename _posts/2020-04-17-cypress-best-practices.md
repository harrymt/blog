---
layout: post
title: 7 Best Practices for Cypress
tags:
  - cypress
  - typescript
---

I recently refactored and improved a large test suite library that used Cypress as the main test automation tool.
Here are some best practices and common mistakes I found for working with this library.

1. [Selecting Elements](#1-selecting-elements)
2. [Unnecessary Wait](#2-unnecessary-wait)
3. [Cucumber Steps](#3-cucumber-steps)
4. [Cypress Commands](#4-cypress-commands)
5. [User Permissions](#5-user-permissions)
6. [Control Data](#6-control-data)
7. [How to Debug Failing Tests](#7-how-to-debug-failing-tests)

### Cypress

Find out more information at [Cypress.io](https://www.cypress.io/).

## 1. Selecting Elements

Use `cy.contains()`, with regex to for an exact match and avoid capitalisation with CSS as it makes this difficult to write tests against.

If you have text that you want to change but you don't want to break the cypress test, then you can use `data-cy` selectors, but this shouldn't be the go to!

![Selecting Elements in Cypress]({{site.baseurl}}/img/cypress-1.png)
> [https://docs.cypress.io/guides/references/best-practices.html#Selecting-Elements](https://docs.cypress.io/guides/references/best-practices.html#Selecting-Elements)

## 2. Unnecessary Wait

Don't use `wait()`.

Cypress will retry the previous command if an assertion fails and will keep doing this until the global timeout is reached.

If you need to wait for an action, there are assertions you can use to wait for an element to not exist, e.g. `cy.contains('Successfully uploaded').should('not.exist')`.

A classic example is waiting for a toast notification to disappear before taking a visual snapshot.

![Selecting Elements in Cypress]({{site.baseurl}}/img/cypress-2.png)

> [https://docs.cypress.io/guides/core-concepts/retry-ability.html#Commands-vs-assertions](https://docs.cypress.io/guides/core-concepts/retry-ability.html#Commands-vs-assertions)
> [https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting](https://docs.cypress.io/guides/references/best-practices.html#Unnecessary-Waiting)

## 3. Cucumber Steps
This project used Cucumber integration and I found creating a lot of generic cucumber selectors helped with writing tests.

Search for these before writing your own!

Be sure that each feature file should be self contained and can be independently verified.

> [https://www.npmjs.com/package/cypress-cucumber-preprocessor](https://www.npmjs.com/package/cypress-cucumber-preprocessor)

## 4. Cypress Commands

Use existing Cypress commands that are already written instead of creating more.

In this project we decided to use ES6 classes with static methods instead of writing more Commands. This worked better for adding Typescript support later on.

## 5. User Permissions

Try to login as users with different permissions instead of a super user that has all permissions.

## 6. Control Data

Mock or control test data as much as possible.

This helps tests to not flake and be easily reproducible locally.

Some tests even go as far as filtering tables for a unique name that is used only in a single test.

## 7. How to Debug Failing Tests

Our tests were uploaded to Circle CI, to debug the failing tests, follow these steps:

1. Tests tab
2. Artifacts Tab
3. Search for 'failed' and 'diff'


--

Overall I would say that Cypress has been the best automation tool I have used and even when we evaluated other alternatives, such as [Taiko, by Gauge](https://github.com/getgauge/taiko), we found that Cypress was the most mature and supported all our use cases.
