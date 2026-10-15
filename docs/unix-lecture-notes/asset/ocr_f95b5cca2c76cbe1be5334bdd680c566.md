# B.5.0.3 Command Separators and Multitasking

Commands can be combined on single lines by using command separators. The semicolon ";" acts like a newline character to the shell – it terminates the preceding command, as in:

```
$ ls mydir ; date
```

which lists the contents of the given directory and then displays the current time and date. The date command displays the date and time in various formats, but by default its output is in the form

```
Mon Aug 15 22:53:54 EDT 2011
```

The semicolon ";" is used to sequentially execute the commands. In contrast,

```
$ ls mydir > outfile &
```

causes the ls command to work "in the background." The ampersand "&" at the end of the line tells the shell not to wait for the command to terminate but to instead resume immediately; it is a backgrounding operator. The ls command runs in the background, sending its output to the file outfile while the shell does other things. This is a form of multitasking. The "&" can be used to run separate commands as well:

```
$ ls mydir > outfile1 & date > outfile2 &
```

tells the shell to run the ls and date commands concurrently and in the background, putting their respective outputs in files outfile1 and outfile2 respectively. Note that the ">" binds more closely, i.e., has higher priority, than "&". Lastly, parentheses can be used for grouping:

```
$ (ls mydir; date) > outfile &
```

means "execute ls mydir, then date, and direct their combined output to outfile," all in the background.

# B.5.0.4 The Shell as a Command

Shells can be run as commands. You can type the name of a shell, e.g., bash, sh, csh, etc., at the command prompt within any other shell, to start another shell:

```
$ sh
```

in this case the Bourne shell. If you do this, you will have two instances of the bash shell running, but the first will be dormant, waiting for the second to exit. When one shell is created as a result of a command given in another shell, the created shell is called the sub-shell of the original shell, which is called the parent shell.

If you need to know what shell you are currently running (because you forgot, for example), there are two simple commands that can tell you: