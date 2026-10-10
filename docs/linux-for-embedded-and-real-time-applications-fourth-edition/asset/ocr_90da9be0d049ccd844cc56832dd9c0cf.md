Next, we will want to run `netserve` on the target with `netclient` running on the host. Delete `netserv.e.o`, and build the make target for the remote server.

In the terminal window connected to the target (the one running `ssh`), `cd` to the `network/` directory and execute `./netserve`. Back in the original window, execute `./netclient remote`.

# ### A Remote Thermostat

Moving on to a more practical example, our thermostat may very well end up in a distributed industrial environment where the current temperature must be reported to a remote monitoring station, and setpoint and limit need to be remotely settable. Naturally we will want to do that over a network.

Copy `monitor.c` and `thermostat.c` from the `Posix/` directory to `network/`, and do a Refresh on the network project to bring those files into Eclipse. Actually, `thermostat.c` does not require any changes. Here are the modifications required in `monitor.c`:

+   1.  Isolate the process of setting up the net server and establishing a connection in a separate function called `createServer()`, which consists roughly of lines 18 to 55 from `netserv.e.c`. The reason for doing it this way will become apparent soon. `createServer()` takes no arguments, and returns an `int` that is the socket number returned by `accept()`. It should return a `-1` if anything fails.
+   2.  Call `createServer()` from `monitor()` just before the `while (1)` loop, and check the return value for error.
+   3.  Replace `fgets()` with `read()` on the socket returned by `createServer()`.
+   4.  Add a new command to the `switch` statement, `“?”`, that returns the current temperature over the network. Actually, we might want to query any of the thermostat’s parameters. Think about how you might extend the command protocol to accomplish that.
+   5.  The `netclient` expects a response string for every string it sends to the server. So return `"OK"` for every valid parameter change command, and return `"???"` for an invalid command.

Create make targets for both the simulation and target versions of the thermostat. Build the simulation version, and point the host debug configuration at `network/thermostat_s`. You will need two shell windows to exercise the thermostat; one for the `devices` program and the other for `netclient`.

When you are satisfied with the simulation, build the target version, and try it there. Remember to delete `thermostat.o` and `monitor.o^{3}` before rebuilding. Also remember to execute `netclient remote`, to get the client talking to the server on the target.

³ There should be a way to do this automatically in the makefile, but I haven’t figured it out yet.