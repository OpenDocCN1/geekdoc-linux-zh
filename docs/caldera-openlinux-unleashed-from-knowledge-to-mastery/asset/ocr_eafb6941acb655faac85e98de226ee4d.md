# Example 3.5
$ ls /usr
X11R6/ dict/ games/ include/ java/ libexec/ man/ sbin/ src/
bin/ doc/ i386-linux/ info/ lib/ local/ openwin/ share/
$ ls /usr/var/
adm/ catman/ lib/ lock/ log/ nis/ run/spool/ state/ tmp/

# I/O Redirection

Data presented to or produced by UNIX shells is separated into one of three categories--stdin, stdout, or stderr. These data can be directed by using the > and < characters to a file or command you want to manipulate or store the data in.

+   * **stdin** Standard input is the input a command receives and is represented by <.
+   * **stdout** Standard output is the output a command produces and is represented by >. (It is technically the first file descriptor, so it can also be represented by 1> or 1 see the following discussion.)
+   * **stderr** Standard error is the output a command produces on error and is represented by >. (It is the second file descriptor.)

# Example 3.6 stdout to a file
$ command > file
$ command 1> file
$ command >! file [This is a clobber redirection]

In this example, you can see stdout at work. The output of command is directed to file. The significance of the > in the third line is that it will "clobber" the file. In other words, the shell will not check whether you had intended to destroy an already existing file; it will just write to it. (This normally only matters if you had previously set the noclobber shell variable.)

# Example 3.7 Appending stdout
$ command >> file

This shows appending stdout to a file. If file already exists and contains data you want to keep, you can add the output of command to file by appending with >>.

# Example 3.8 Redirecting stdin
$ command < file