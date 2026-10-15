# EXAMPLE 11.66 (CONTINUED)

```
5 Hello there ellie
The time is Sun May 30 19:42:16 PDT 2004
I can't wait to see you!!
6 $

```

# EXPLANATION

+   1. The UNIX/Linux cat program will accept input until the word FINISH appears on a line by itself. FINISH is called a user-defined terminator.
+   2. Variable substitution is performed within the here document. The > is the Korn shell's secondary prompt.
+   3. Command substitution is performed within the here document.
+   4. The user-defined terminator, FINISH, marks the end of input for the cat program. It cannot have any spaces before or after it and is on a line by itself.
+   5. The output from the cat program is displayed.
+   6. The shell prompt reappears.

# EXAMPLE 11.67

```
(From the .profile File)
1 print "Select a terminal type"
2 cat << EOF
[1] sun
[2] ansi
[3] wyse50
3 EOF
4 read TERM
...
```

# EXPLANATION

+   1. The user is asked to select a terminal type.
+   2. The menu will appear on the screen. This is a here document, meaning from here until the matching EOF on line 3 is reached, input will be given to the cat command. You could use a series of echo commands to get the same results, but visually, the here document is nicer.
+   3. EOF is a user-defined terminator, marking the end of the here document. It must be at the left margin with no spaces surrounding it.
+   4. The user input will be read in from the keyboard and assigned to TERM.