
In this sequence, you first sent signal `19`, which is `SIGSTOP` (stop), followed by signal `18`, which is `SIGCONT` (continue). Given the output of `jobs`, this should now make more sense.

You can see a list of all signals with `kill -L`.

## Task 2:

Now create a few `sleep` processes if you haven't already, and use either `killall` or `pkill` to terminate them all with a single command. Both commands have the same general function, with slightly different arguments, so it's worth experimenting with and reading the man pages for both.

## Notes:

`pkill` and `pgrep` have exactly the same searching/matching semantics. This means you can use `pgrep` as a "dry run" to find the processes you want to signal before actually doing so.
