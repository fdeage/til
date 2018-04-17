# RSPEC

- before eagerly runs code before each test.
- let lazily runs code when it is first used (let is used for memoization - as a kind of helper/function) -> one statement per let
- Use before for actions, let for dependencies (real or test double)
- before to initialize things, let for dependencies/things that might be active already


[before and let in TDD](https://www.launchacademy.com/codecabulary/learn-test-driven-development/rspec/before-vs-let)


- describe and context are THE SAME METHOD (aliased), except context isn’t available at top level
- Use describe for things, use context for states
- context names should not match your method names, but explain why a user would call the method


Test::Unit : native Ruby code, test classes (13 methods everything included)
RSpec : you are looking to combine ‘expectations’ with ‘matchers’. Fat