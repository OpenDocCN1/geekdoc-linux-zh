
You should see the numbers `0-9` printed out, one at a time. Knowing what the script does now, can you understand it in its entirety? What happens if you fail to pass an argument, or if you pass `"gibberish"` like letters instead of a number?

## Task 3

Run your script without an argument. Then run:
```
echo $?
```

`$?` is a special variable that references the exit status. In a successful program, the exit status would be `0`. Please try it for yourself now. Then edit the script by removing the last `echo` statement. This script then fails without an argument, returning a different exit status.

## Notes

That first line, starting with `#!` (called a shebang), denotes what program will be used to interpret your script. Usually, this is `/bin/bash`, but it can also be another shell like `/bin/zsh`, or even another programming language like `/usr/bin/python`.

In this case, you could remove the shebang line, because your interpreter is the same (`Bash`) as the shell you are currently running. But you should always include it because you never know when you might want to share a script with someone using a different shell.
