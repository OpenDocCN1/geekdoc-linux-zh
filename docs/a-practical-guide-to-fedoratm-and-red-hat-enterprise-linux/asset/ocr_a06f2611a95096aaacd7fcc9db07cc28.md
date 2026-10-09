# exec: REDIRECTS INPUT AND OUTPUT

The second major use of **exec** is to redirect a file descriptor—including standard input, output, or error—from within a script. The next command causes all subsequent input to a script that would have come from standard input to come from the file named *infile*:

```
exec < infile
```

Similarly the following command redirects standard output and standard error to *outfile* and *errfile*, respectively:

```
exec > outfile 2> errfile
```

When you use **exec** in this manner, the current process is not replaced with a new process and **exec** can be followed by other commands in the script.

**/dev/tty** When you redirect the output from a script to a file, you must make sure the user sees any prompts the script displays. The */dev/tty* device is a pseudonym for the screen the user is working on; you can use this device to refer to the user’s screen without knowing which device it is. (The *tty* utility displays the name of the device you are using.) By redirecting the output from a script to */dev/tty*, you ensure that prompts and messages go to the user’s terminal, regardless of which terminal the user is logged in on. Messages sent to */dev/tty* are also not diverted if standard output and standard error from the script are redirected.

The to_screen1 script sends output to three places: standard output, standard error, and the user’s screen. When run with standard output and standard error redirected, to_screen1 still displays the message sent to */dev/tty* on the user’s screen. The out and err files hold the output sent to standard output and standard error, respectively.

```
$ cat to_screen1
	echo "message to standard output"
	echo "message to standard error" 1>62
	echo "message to screen" > /dev/tty

$ ./to_screen1 > out 2> err
message to screen
$ cat out
message to standard output
$ cat err
message to standard error
```

The following command redirects standard output from a script to the user’s screen:

```
exec > /dev/tty
```

Putting this command at the beginning of the previous script changes where the output goes. In to_screen2, **exec** redirects standard output to the user’s screen so the > */dev/tty* is superfluous. Following the **exec** command, all output sent to standard output goes to */dev/tty* (the screen). Output to standard error is not affected.