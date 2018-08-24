# Basics of OTP


Supervisor, GenServer, Agent, and Task

## What is a process?

In IEx, we can use
```
iex(1)> spawn(fn -> IO.puts("Hello OTP") end)
Hello OTP
#PID<0.409.0>
iex(2)> pid = spawn(fn -> IO.puts("Hello OTP") end)
Hello OTP
#PID<0.411.0>
iex(3)> Process.alive?(pid)
false
```
to create a new process (that dies immediately).

Supervisors are also processess. Their main purpose is to monitoring other processes. If a child process fails, then the supervisor restarts it with a fresh state.


OTP allow us to configure how supervisors will handle failures. For example,

- Whether or not to restart the process
- Restart only the process that failed or all processes linked to the supervisor
- Restarting just when the child process terminates abnormally

These configurations are called Strategies.

## GenServer

GenServer is an implementation for starting and handling all in and out messages in your process.

We only need to  `use GenServer` in our module and implement the 3 following functions:

`GenServer.start(__MODULE__, :ok, [])`

This triggers an `init` function in the module. This function sets the initial process state.

`handle_cast()`

This casts any message that we receive. The message will be pattern-matched with any `handle_cast()` function declared in our module. At the end of this function we return a two-element tuple `{:noreply, new_state}` to give a new state to our server.

`handle_call()`

This sends any message back the the process that pinged us. At the end, we reply with a three-element tuple {:reply, state_to_reply, new_state} where the second element is actually the message that we will send back, and the third one is the new state for our process.
