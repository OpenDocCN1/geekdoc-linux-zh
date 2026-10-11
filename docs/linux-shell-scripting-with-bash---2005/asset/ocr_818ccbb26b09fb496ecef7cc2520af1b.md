Signals are sent to scripts with the built-in `kill` command. Despite what its name implies, `kill` can do more than just terminate programs with its default `SIGTERM` signal. Suppose a slow command is running in the background.

```
$ ( sleep 60; echo "DONE"; ) &
[1] 7613
```

The `kill` command can suspend the command using the `SIGSTOP` signal.

```
$ kill -SIGSTOP 7613
[1]+ Stopped                ( sleep 60; echo "DONE"; )
```

After the command is stopped, it remains inactive until it receives another signal, such as `SIGCONT`.

```
$ kill -SIGCONT 7613
$ DONE
[1]+ Done                    ( sleep 60; echo "DONE"; )
```

The `SIGCONT` signal continues execution at the point of interruption. Linux defines 63 different signals. The signals most commonly sent to scripts are `SIGTERM` (immediately exit the script), `SIGSTOP` (stop the script, putting it to sleep temporarily), `SIGHUP` (hang up a connection), and `SIGCONT` (continue a stopped script). A complete list appears in Appendix E, “Signals.”

The built-in `disown` command affects how signals are shared with background tasks. If the `-h` (`SIGHUP`) switch is used, Bash does not share `SIGHUP` with the background jobs of a particular task when a `SIGHUP` is received (such as when a user logs out).

# ## The suspend Command

The built-in `suspend` command stops a script until a signal is received, just as if the script received a `SIGSTOP` signal. It is equivalent to using the command `kill -SIGSTOP $$` to force the script to stop itself. When used in a script, `suspend` requires job control to be enabled. See Listing 10.1.

```
**Listing 10.1** `suspend_demo.sh`
```bash
#!/bin/bash
#
# suspend_demo.sh
#
# Wait for a SIGCONT signal and then print a message
#
# Turn off shell settings that interfere with script execution.
# Specifically, we turn off the nounset and monitor settings.
# This is because we need to be able to handle the SIGCONT signal,
# and the monitor setting interferes with that.
shopt -s -o nounset
shopt -s -o monitor # enable job control

# wait for SIGCONT
```
```