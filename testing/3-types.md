# 3 types of testing

## Unit Testing
- testing small pieces of code, typically individual functions, alone and isolated
- easy to write and maintain
- can be written before writing the body of function: basics of TDD (“red/green/refactor”)
- if the test uses some external resource (network, DB) -> integration test
- backbone of testing. Code that’s hard to unit test usually has poor design. UT should be the main focus (measured by “code coverage”)

## Integration testing
- test how components of the system work together to detect interface defects
- not isolated from other components like UT
- often slower than unit tests because of the added complexity (might also need some set up or config: setting up of a test database, etc.)
- harder to maintain than unit tests, mainly useful where unit testing is not enough: to be written only when necessary

## Functional Testing (= E2E testing, browser testing, acceptance testing, behavior testing…)
- verify that a system meets external requirements by testing complete functionalities/user interactions of an app
- not concerned with intermediate results or side-effects, or any knowledge of the internal working of the system
- very difficult to write and maintain (views, etc.), usually slower to run: have only the minimum


## The 6 steps of TDD
1. decide the inputs and outputs
2. write function signature\
3. write the simplest answer/behavior
4. write tests
5. write code that goes green
6. refactor
