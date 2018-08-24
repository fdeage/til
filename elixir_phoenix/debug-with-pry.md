# Debug with Pry

`Apex.ap` sucks badly for debugging. It's too general and prints huge blobs of undecipherable data.

So instead of 
`MIX_ENV=test mix test test/`,

use
`MIX_ENV=test iex -S mix test test/`

Then on top of the module:
`require IEx`

And in the code itself, add
`IEx.pry`

During debugging, when offered the option
```
Allow? [Yn]
```, press `Y` to enter debugging, or `n` to pass.

(Try also `respawn`)
