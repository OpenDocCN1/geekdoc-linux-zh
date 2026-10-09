# Determining Whether a File Descriptor Is Associated with the Terminal

The `test -t` criterion takes an argument of a file descriptor and causes `test` to return a value of 0 (true) or not 0 (false) based on whether the specified file descriptor is associated with the terminal (screen or keyboard). It is typically used to determine whether standard input, standard output, and/or standard error is coming from/going to the terminal.

In the following example, the `is.term` script uses the `test -t` criterion ([1] is a synonym for `test`; page 1000) to see if file descriptor 1 (initially standard output) of the process running the shell script is associated with the screen. The message the script displays is based on whether `test` returns true (file descriptor 1 is associated with the screen) or false (file descriptor 1 is *not* associated with the screen).

```
$ cat is.term

if [ -t 1 ]; then

	echo "FD 1 (stdout) IS going to the screen"

else
	echo "FD 1 (stdout) is NOT going to the screen"

fi
```

When you run `is.term` without redirecting standard output, the script displays **FD 1 (stdout) IS going to the screen** because standard output of the `is.term` script has not been redirected:

```
$ ./is.term

FD 1 (stdout) IS going to the screen
```

When you redirect standard output of a program using > on the command line, `bash` closes file descriptor 1 and then reopens it, associating it with the file specified following the redirect symbol.

The next example redirects standard output of the `is.term` script: The newly opened file descriptor 1 associates standard output with the file named `hold`. Now the `test` command (`[ -t 1]`) fails, returning a value of 1 (false), because standard output is not associated with a terminal. The script writes **FD 1 (stdout) is NOT going to the screen** to `hold`:

```
$ ./is.term > hold
$ cat hold
FD 1 (stdout) is NOT going to the screen
```

If you redirect standard error from `is.term`, the script will report **FD 1 (stdout) IS going to the screen** and will write nothing to the file receiving the redirection; standard output has not been redirected. You can use `[ -t 2 ]` to test if standard error is going to the screen:

```
$ ./is.term 2> hold
FD 1 (stdout) IS going to the screen
```