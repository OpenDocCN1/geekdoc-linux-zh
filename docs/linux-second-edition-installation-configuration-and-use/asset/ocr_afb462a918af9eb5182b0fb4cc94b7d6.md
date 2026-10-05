# 392 THE BASH - A MODERN COMMAND INTERPRETER

alias calls can also be embedded. Please note that alias abbreviations precedence over commands bearing the same name. This can be used to prevent
unwanted calls of commands:

```
user$ aliasless
```

From now on, each attempt to call the more command leads to the start of the
more powerful, but otherwise equivalent, program less. If you really need more, you
specify the complete path (/bin/more).

alias abbreviations can be deleted with unalias. Otherwise, they remain valid\until you exit the shell (that is, at most until you log out). If you need specific-
abbreviations more frequently, you may incorporate their alias instructions into the
.profile file in your home directory.

A similar effect can be achieved with shell programs under a concise
file name. Shell scripts have the additional advantages that they can cope with
parameters ($1, $2, and that they can be employed in a much more
flexible way (see page 405).

![](bbox=[0.218, 0.305, 0.258, 0.375])

# 12.3 Input and output redirection

Three so-called standard files are involved in every command execution in the bash.
The term 'file' might be slightly misleading; precisely speaking, 'standard files'
are not true files, but file descriptors that can be treated as files at operating system
level.

+   - Standard input: this is where currently executing programs read their input (for
example, when text is entered into an editor). In general, the standard input is
the keyboard.

+   - Standard output: this is where all program output is directed (for example,
listing of all files through ls). In general, the standard output is the screen (the
current terminal or, under X, the current terminal window).

+   - Standard error: error messages are generally displayed on the current-
terminal.

It is desirable that the three standard files are changed when certain com-
mands are executed. For example, the contents list of the current directory may have
to be written to a file instead of being displayed on screen. Thus, the standard out-
out must be redirected into a true file. In the bash, this is achieved through the >
character:

```
user$ ls *.tex > contents
```

Now, the text file contents contains a list of all *.tex files in the current-
directory. This form of output redirection is certainly the most frequent application.
There are a number of further variations: 2> file directs all error messages into the
specified file. > file directs both the standard output and the error messages into