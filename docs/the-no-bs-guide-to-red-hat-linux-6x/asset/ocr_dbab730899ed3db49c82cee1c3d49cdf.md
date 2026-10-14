# The Case Statement

Most languages provide a case or switch statement that lets you compare a string with several possible values and execute a block of code when a match is found. Perl does not, but it does provide a way to implement this procedure. Here’s an example of the SWITCH construct, with the syntax shown in boldface and the parts you would supply in normal type:

```
SWITCH: {
  if ( $A eq "ls" )  { system("ls"); last SWITCH; }
  if ( $A eq "pwd" ) { system("pwd"); last SWITCH; }
  if ( $A eq "date" ) { system("date"); last SWITCH; }
  print "none of the args were very interesting. \n";
}
```

In this example, if the value of $A was ls, the first block of commands would execute. If the value of $A was pwd, the second block of commands would execute. Otherwise, the rest of the commands in the SWITCH clause would execute. The last SWITCH command tells Perl to short-circuit the rest of the stuff in the SWITCH clause, so as soon as one of the conditions is satisfied, the others are ignored.

# LOOPING

Shell scripts written in Bash can implement looping, or iteration, with the while, until, and for constructs. In each case, a block of code is executed repeatedly until a loop exit condition is satisfied. The script then continues on from that point.

# The While Statement

In a while loop, the block of code between the { and } braces is executed so long as the conditional expression is true. Think of it as saying, “Execute while this condition remains true.” Here’s an example:

```
while ($ARG) {
  print "ARG: $ARGV[0] \n";
  shift $ARGV;
}
```

This trivial example prints the value of each argument passed to the shell script. Translated to English, the while condition says to continue so long as the input argument string is not null. You might think that this loop would continue to print the first argument $ARGV[0] forever and ever, since you don’t expect the value of the @ARGV variable (the