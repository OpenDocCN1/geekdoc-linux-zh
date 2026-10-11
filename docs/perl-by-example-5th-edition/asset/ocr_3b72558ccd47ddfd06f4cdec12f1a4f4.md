# EXPLANATION

1 The system function executes the UNIX *cal* command to print out the calendar for the month of January 2015.

2 The system function executes the Windows *notepad.exe* command and starts up a session of Notepad.

# EXAMPLE 16.59

(The Script)

```
1 print "Hello there\n";
2 print "The name of this machine is ";
3 system ("uname -n"); # Buffer is not flushed
4 print "The time is ", `date`;
```

(Output)

```
1 Hello there
3 jody
2,4 The name of this machine is The time is Tue May 29 13:39:35 PDT 2007
```

# EXPLANATION

1 The first *print* statement is executed as expected.

2 Since Perl depends on the default I/O buffering mechanism, the buffer may not be flushed immediately after the *print* statement; the results of the *system* function, executed by the shell, are printed first.

3 The *system* function causes the shell to execute the UNIX command *uname -n*.

4 This *print* statement is printed directly after the *print* statement in line 2.

# EXAMPLE 16.60

(The Script)

```
use warnings;
1 $| = 1; # Set special variable to flush the output buffer
2 print "Hello there\n";
3 print "The name of this machine is ";
system ("uname -n");
4 print "The time is ", `date`;
```

(Output)

```
2 Hello there
3 The name of this machine is jody
4 The time is Mon Jan 26 13:43:54 PST 2015
```

# EXPLANATION

1 The $| special variable, when set to nonzero, forces the output buffer to flush after every *write* or *print*.