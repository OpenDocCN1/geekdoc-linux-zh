**The** `echo $0` **command shows the current shell in use only when issued at a shell prompt. If used in a shell script, it will display the script's name instead. This is covered in Chapter 14, “Handling User Input.”**

With our handy `$0` variable, we'll display the shell we are currently using, start the Dash shell by typing the command **dash**, and show the new shell's name via `echo $0` again:

```
```
$ echo $0
-bash
$
$ dash
$
$ echo $0
dash
$
```
```

# NOTE

**In the previous example, notice the dash (-) in front of the bash response from the first** `echo $0` **command. This indicates that this shell is the user's login shell.**

The $ prompt is a CLI prompt for the Dash shell. You can leave the Dash shell program (and the Bash shell for that matter) by typing the command `exit`:

```
```
$ echo $0
dash
$ exit
$ echo $0
-bash
$
```
```

Jumping back and forth through the various shells seems simple, but there is more to the action happening behind the scenes. To understand this process, the next section explores the relationship between a login shell program and a newly started shell program.