# Phoenix testing

## EX vs EXS
The only difference is in intention. .ex files are meant to be compiled while .exs files are used for scripting.

## Tests
ExUnit tests are run in a random order via a seed integer.

## Private functions
There is no way to test them via ExUnit.

Avoid testing private functions: usually you end up testing implementation instead of behaviour and those tests fail as soon as you need to change the code. Instead, I test the expected behaviour via the public functions, breaking them in small, consistent chunks.

## Modules
- Assertions:  assert, assert_raise, assert_receive, refute, refute_receive
- Callbacks: setup, setup_all, on_exit
- Capture: capture_io / capture-log
- Case: describe, test (+ context, not-implemented, ...), tags
- CaseTemplate
- Filters: RAS
- Test (keeping info on the test): 
t() :: %ExUnit.Test{case: module, logs: term, name: atom, state: ExUnit.state, tags: map, time: non_neg_integer}
