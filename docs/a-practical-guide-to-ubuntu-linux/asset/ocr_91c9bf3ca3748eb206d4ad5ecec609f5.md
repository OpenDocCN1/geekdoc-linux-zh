# 1008 CHAPTER 27 PROGRAMMING THE BOURNE AGAIN SHELL

Similarly the following command redirects standard output and standard error to outfile and errfile, respectively:

```
exec > outfile 2> errfile
```

When you use exec in this manner, the current process is not replaced with a new process, and exec can be followed by other commands in the script.

/dev/tty When you redirect the output from a script to a file, you must make sure the user sees any prompt script displays. The /dev/tty device is a pseudonym for the screen you are working on; you can use this to refer to the user's screen without knowing which device it is. (The tty displays the name of the device you are using.) By redirecting the output from a script to /dev/tty, you ensure that prompts go to the user's terminal, regardless of which terminal the user is logged in. Messages sent to /dev/tty are not diverted by standard output and standard error from the script are redirected.

The to_screen1 script sends output to three places: standard output, standard error, and the user's. When run with standard output and standard error redirected, to_screen1 still displays the message to /dev/tty on the user's screen. The out and err files hold the output sent to standard output and standard error.

```
$ cat to_screen1
echo "message to standard output"
echo "message to standard error" 1>&2
echo "message to the user" >/dev/tty
```

```
$ /to_screen1 > out 2> err
message to the user
$ out
message to standard output
$ err
message to standard error
```

The following command redirects the output from a script to the user's screen:

```
exec > /dev/tty
```

Putting this command at the beginning of the previous script changes where the output puts. In to_screen2, exec redirects standard output to the user's screen so > /dev/tty is superfluous. Following the exec command, all output sent to standard output goes to /dev/tty (the screen). Output to standard error is not affected.

```
$ cat to_screen2
exec > /dev/tty
echo "message to standard output"
echo "message to standard error" 1>&2
echo "message to the user" > /dev/tty
```

```
$ /to_screen2 > out 2> err
message to standard output
message to the user
```

One disadvantage of using exec to redirect the output to /dev/tty is that all subsequent output is redirected unless you use exec again in the script.