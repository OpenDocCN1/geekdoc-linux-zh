\h is the first part of the hostname (such as mysystem)

\u is the username

\t is the time in 24-h format

The complete list of strings can be found in the documentation, including how to add colors and sounds (which may be useful to highlight the fact that you are operating at the root level, or, for system administrators, which machine you are actually logged onto). Modifying the variable as above will not make it permanent, and will revert back to the system setting when the user logs off and then back on again. To make the changes permanent, they have to be included in your local profile.

# PS2

The PS2 variable is very similar to the PS1 variable, except that it is displayed when the user issues an incomplete command and the system will prompt and wait for the user to complete the command and press enter again. This default secondary prompt is the > sign and can be changed by altering the PS2 variable.

```
$ echo ``this is a
> test''
this is a
test
$

Redefining the PS2 variable with a customized prompt is shown below:

$ PS2='''more input > ''
$ echo ''this is a
more input > test''
this is a
test
$
```

> **Note**
> There are other prompt string variables available in some shells, such as PS3 and PS4 in the Korn shell. These are not specifically required in the exam due to their specific nature.

# Path

The PATH variable is used by commands to locate a specific command or application. When you enter a command, the shell will look in each of the