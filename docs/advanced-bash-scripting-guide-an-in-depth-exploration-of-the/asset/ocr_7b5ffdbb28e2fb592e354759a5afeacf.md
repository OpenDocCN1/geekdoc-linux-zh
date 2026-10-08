# Advanced Bash-Scripting Guide

+   * A script with DOS-type newlines (\r\n) will fail to execute, since #!/bin/bash\r\n is not recognized, not the same as the expected #!/bin/bash\n. The fix is to convert the script to UNIX-style newlines.

```
```bash
#!/bin/bash
echo "There"
unix2dos $0
chmod 755 $0
## Script changes itself to DOS format.
# Change back to execute permission.
# The 'unix2dos' command removes execute permission.

./$0
## Script tries to run itself again.
# But it won't work as a DOS file.

echo "There"
exit 0
```
```

A shell headed by #!/bin/sh will not run in full Bash-compatibility mode. Some Bash-specific functions might be disabled. Scripts that need complete access to all the Bash-specific extensions should start with #!/bin/bash.

+   * Putting whitespaces in front of the terminating limit string of a here document will cause unexpected behavior in a script.

+   * Putting more than one statement in a script whose output is captured.

```
```bash
add2() {
  echo "Whatever"  # Delete this line!
  let retval = $1 + $2
  echo $retval
}

num1=12
num2=43
echo "Sum of $num1 and $num2 = $(add2 $num1 $num2)"

# Sum of 12 and 43 = Whatever
# 55

#  The "echoes" concatenate.
```
```

This will not work.

A script may not export variables to its parent process, the shell, or to the environment. Just as we learned in biology, a child process can inherit from a parent, but not versa.

```
```bash
WHATE=/home/bozo
export WHATE
exit 0
bash$ echo $WHATE
bash$
```
```

Sure enough, back at the command prompt, $WHATE remains unset.

+   * Setting and manipulating variables in a subshell, then attempting to use those same variables outside the scope of the subshell will result in unpleasant surprise.

Chapter 34. Gotchas

494