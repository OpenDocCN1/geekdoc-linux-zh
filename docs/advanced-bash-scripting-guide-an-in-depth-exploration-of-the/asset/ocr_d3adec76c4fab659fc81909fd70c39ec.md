# Advanced Bash-Scripting Guide

```
let "z = 5 % 3*"
echo $ # 2
```

In a different context, the % is a pattern matching operator.

home directory [tilde]. This corresponds to the $HOME internal variable. ~bozo is bozo's home directory, and ~bozo lists the contents of it. ~/ is the current user's home directory, and ~ls lists the contents of it.

```
bash$ echo -bozo
/home/bozo

bash$ echo ~
/home/bozo/

bash$ echo ~:
/home/bozo:

bash$ echo -nonexistent-user
-nonexistent-user
```

current working directory. This corresponds to the $PWD internal variable.

previous working directory. This corresponds to the $OLDPWD internal variable.

regular expression match. This operator was introduced with version 3 of Bash.

beginning-of-line. In a regular expression, a "^" addresses the beginning of a line

Uppercase conversion in parameter substitution (added in version 4 of Bash).

change the behavior of the terminal or text display. A control character is a CONTROL + key combination (pressed simultaneously). A control character may also be written in octal or hexadecimal notation, following an escape.

Control characters are not normally useful inside a script.

+   - ◇ Ctrl-A
  Moves cursor to beginning of line of text (on the command-line).
- ◇ Ctrl-B
  Backspace (nondestructive).
- ◇ Ctrl-C
  Break. Terminate a foreground job.
- ◇ Ctrl-D

Chapter 3. Special Characters

25