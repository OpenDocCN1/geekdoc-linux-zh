**The Output Filter.** When creating a handle with the open function, you can open a filter so that the output is piped to a system command. The command is preceded by a pipe symbol () and replaces the filename argument in the previous examples. The output will be piped to the command and sent to STDOUT (see Figure 10.2). You can use the two-argument format or the three-argument format, as shown in the following example. With the three-argument format, your shell (bash, korn, and so on) may be avoided and, thus, shell wildcard expansion, redirection, and multistage pipelines will not be handled.

# FORMAT

```
open(PIPE, "|COMMAND");
open ($pipe, "|-", "COMMAND");
```

# EXAMPLE 10.30

```
(The Script)
use warnings;
# Scriptname: outfilter (UNIX/Windows)
1 open(MYPIPE, "|sort");
2 print MYPIPE "dogs\ncats\nbirds\nzebras\n";
3 close(MYPIPE);
4 open (my $mypipe, "|-", "sort" ); # Three-argument format
5 print $mypipe "dogs\ncats\nbirds\nzebras";
6 close $mypipe;

(Output)
birds
cats
dogs
zebras

birds
cats
dogs
zebra
```

# EXPLANATION

+   1. The user-defined pipe handle MYPIPE will be used to pipe output from the Perl script to the OS command sort, which sorts lines, hence the newline between each animal.
+   2. The print function sends the output to MYPIPE instead of to the screen. The sort command on right-hand side of the pipe sorts by lines.
+   3. After you have finished using the pipe handle, close it. This guarantees that the command will complete before the script exits. If you don't close the handle, the output may not be flushed properly.
+   4. This is the three-argument style for creating a pipe. The pipe name is a lexical scalar, $mypipe, the pipe symbol with a dash on its right-hand side, |-, indicates that Perl will be sending output to the pipe where the OS sort command is represented by the dash. Perl writes; the sort command reads.