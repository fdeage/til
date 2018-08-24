# Enable history in IEX through #erlang (OTP 20)

If you are using the latest version of Erlang, OTP 20 now ships with shell history (Ctrl-p / Ctrl-n or the up/down arrow keys).

The shell history is turned off by default though, so you will have to turn manually by setting this env variable:
```export ERL_AFLAGS="-kernel shell_history enabled"```
