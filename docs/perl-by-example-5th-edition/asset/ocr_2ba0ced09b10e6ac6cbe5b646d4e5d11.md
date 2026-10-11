For any text entered at the debugger prompt, leading and trailing whitespace is first stripped before further processing. If a debugger command coincides with some function in your own program, merely precede the function with something that doesn't look like a debugger command, such as a leading ; or perhaps a +, or by wrapping it with parentheses or braces.

<continues here>

# A.6.3 Entering and Exiting the Debugger

To invoke the Perl debugger, use the -d switch. It allows you to examine your program in an interactive-type environment after it has successfully compiled. After each line, the script will stop and ask for a command. The line you will be looking at is the next line that will be executed, not the previous one. The prompt contains the current package, function, file and line number, and the current line. Following is a list of the debug commands.

Once you start the debugger, all the debugging commands are listed by typing h at the debug prompt, or h if you can't read what is displayed.

To exit the debugger, type q for quit or R for restart.

```
```
$ perl -d exer1.
Loading DB routines from $SRCfile: perlDB.pl,v $$Revision: 4.0.1.2
$$Date: 91/11/05 17:55:58 $
Emacs support available.
Enter h for help.
main'(exer1:3):       print "Today is " , $date' ;
DB<1> h
```

```

+   t          Stack trace.
+   s          Single step.
+   n          Next, steps over subroutine calls.
+   r          Return from current subroutine.
+   c [line]   Continue; optionally inserts a one-time-only
+              breakpoint at the specified line.
+   <CR>       Repeat last n or s.
+   1 min+incr        List incr+l lines starting at min.
+   1 min-max         List lines.
+   1 line            List next window.
+   -               List previous window.
+   w line            List window around line.
+   1 subname         List subroutine.
+   f filename        Switch to filename.
+   /pattern?        Search forwards for pattern; final / is optional.
+   ?pattern?        Search backwards for pattern.
+   L               List breakpoints and actions.
+   S               List subroutine names.