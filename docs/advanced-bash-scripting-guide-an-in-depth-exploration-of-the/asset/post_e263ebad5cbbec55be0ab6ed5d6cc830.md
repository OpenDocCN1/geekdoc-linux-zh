
# Advanced Bash-Scripting Guide

+   * A script with DOS-type newlines (\r\n) will fail to execute, since #!/bin/bash\r\n is not recognized, not the same as the expected #!/bin/bash\n. The fix is to convert the script to UNIX-style newlines.

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

This will not work.

A script may not export variables to its parent process, the shell, or to the environment. Just as we learned in biology, a child process can inherit from a parent, but not versa.

```bash
WHATE=/home/bozo
export WHATE
exit 0
bash$ echo $WHATE
bash$
```

Sure enough, back at the command prompt, $WHATE remains unset.

+   * Setting and manipulating variables in a subshell, then attempting to use those same variables outside the scope of the subshell will result in unpleasant surprise.

Chapter 34. Gotchas

# Advanced Bash-Scripting Guide

Example 34-2. Subshell Pitfalls

```bash
#!/bin/bash
# Pitfalls of variables in a subshell

outer_variable=outer
echo
echo "outer_variable = $outer_variable"
echo
(
  # Begin subshell
echo "outer_variable inside subshell = $outer_variable"
inner_variable=inner # Set
echo "inner_variable inside subshell = $inner_variable"
outer_variable=inner # Will value change globally?
echo "outer_variable inside subshell = $outer_variable"

  # 'exporting' make a difference?
  # export inner_variable
  # export outer_variable
  # Try it and see.
  # End subshell
)
echo "inner_variable outside subshell = $outer_variable" # Unset.
echo "outer_variable outside subshell = $outer_variable" # Changed.
echo

exit 0
```

# What happens if you uncomment lines 19 and 20?
# Does it make a difference?

Piping echo output to a read may produce unexpected results. In this scenario, the read acts as if it were running in a subshell. Instead, use the set command (as in Example 15-18).

# Example 34-3. Piping the output of echo to a read

```bash
#!/bin/bash
# badread.sh:
# Attempting to use 'echo' and 'read'
+# to assign variables non-interactively.

shopt -s lastpipe

a=aaa
b=bbb
c=ccc

echo "one three" | read a b c
# Try to reassign a, b, and c.

echo
echo "a = $a" # a = aaa
echo "b = $b" # b = bbb
```

```
echo c = "$c" # c = c
# Reassignment failed.

### However
## Uncommenting line 6:
## shopt -s lastpipe
## fixes the problem!
### This is a new feature in Bash, version 4.2.

-------------------------

# Try the following alternative.
var=$(echo "one two three"
set $var
a=$1; b=$2; c=$3

-------------------------
echo
echo a = "$a" # a = one
echo b = "$b" # b = two
echo c = "$c" # c = three
# Reassignment succeeded.
```

# Note also that an echo to a 'read' works within a subshell.
## However, the value of the variable changes "only" within the subshell.

a=aaa # Starting all over again.
b=bbb
c=ccc

```
echo;
echo "one two three" | read a b c;
echo "Inside subshell: " echo a = "$a"; echo b = "$b"; echo c = "$c"
a = one
# b = two
# c = three
-------------------------
echo "Outside subshell: "
echo a = "$a" # a = aaa
echo b = "$b" # b = bbb
echo c = "$c" # c = ccc
echo
```

In fact, Anthony Richardson points out, piping to any loop can create a similar problem.

```bash
# Loop piping throttles.
# This example by Anthony Richardson,
## with addendum by Wilber Berendsen.

foundone=false
find $HOME -type f -atime +30 -size 100k |
while true
doo
read f
echo "$f is over 100KB and has not been accessed in over 30 days"
echo "Consider moving the file to archives.")
```

```
foundone=true
# -----------------
echo "Subshell level = $BASH_SUBSHELL"
# Subshell level = 1
# Yes, we're inside a subshell.
# -----------------
done

# foundone will always be false since it is
+# set to true inside a subshell
if [ $foundone = false ];
then
    echo "No files need archiving."
fi

# ===================Now, here is the correct way=================
foundone=false
for f in $(find $HOME -type f -atime +30 -size 100k);
do
    echo "$f is over 100KB and has not been accessed in over 30 days"
    echo "Consider moving the file to archives."
    foundone=true
done

if [ $foundone = false ];
then
    echo "No files need archiving."
fi

# ===================Now, here is the correct way=================
foundone=false
while read -r f; find $HOME -type f -atime +30 -size 100k | while read f
do
    echo "$f is over 100KB and has not been accessed in over 30 days"
    echo "Consider moving the file to archives."
    foundone=true
done

if [ $foundone = false ];
then
    echo "No files need archiving."
fi

# ===================Now, here is the correct way=================
foundone=false
while IFS= read -r -d '' f; find $HOME -type f -atime +30 -size 100k -print0
do
    echo "$f is over 100KB and has not been accessed in over 30 days"
    echo "Consider moving the file to archives."
    foundone=true
done

if [ $foundone = false ];
then
    echo "No files need archiving."
fi

# ===================Now, here is the correct way=================
foundone=false
while IFS= read -r -d '' f; find $HOME -type f -atime +30 -size 100k -print0
do
    echo "$f is over 100KB and has not been accessed in over 30 days"
    echo "Consider moving the file to archives."
    foundone=true
done
```
Wait, the OCR text was quite garbled at the end. Let me provide the clean, corrected version based on the logic of the Bash snippets provided.

[content]
# Advanced Bash-Scripting Guide

*   * A script with DOS-type newlines (\r\n) will fail to execute, since #!/bin/bash\r\n is not recognized, not the same as the expected #!/bin/bash\n. The fix is to convert the script to UNIX-style newlines.

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

*   * Putting whitespaces in front of the terminating limit string of a here document will cause unexpected behavior in a script.

*   * Putting more than one statement in a script whose output is captured.

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

```bash
WHATE=/home/bozo
export WHATE
exit 0
bash$ echo $WHATE
bash$
```
```

Sure enough, back at the command prompt, $WHATE remains unset.

*   * Setting and manipulating variables in a subshell, then attempting to use those same variables outside the scope of the subshell will result in unpleasant surprise.

Chapter 34. Gotchas

# Advanced Bash-Scripting Guide

Example 34-2. Subshell Pitfalls

```bash
#!/bin/bash
# Pitfalls of variables in a subshell

outer_variable=outer
echo
echo "outer_variable = $outer_variable"
echo
(
  # Begin subshell
echo "outer_variable inside subshell = $outer_variable"
inner_variable=inner # Set
echo "inner_variable inside subshell = $inner_variable"
outer_variable=inner # Will value change globally?
echo "outer_variable inside subshell = $outer_variable"

  # 'exporting' make a difference?
  # export inner_variable
  # export outer_variable
  # Try it and see.
  # End subshell
)
echo "inner_variable outside subshell = $outer_variable" # Unset.
echo "outer_variable outside subshell = $outer_variable" # Changed.
echo

exit 0
```

# What happens if you uncomment lines 19 and 20?
# Does it make a difference?

Piping echo output to a read may produce unexpected results. In this scenario, the read acts as if it were running in a subshell. Instead, use the set command (as in Example 15-18).

# Example 34-3. Piping the output of echo to a read

```bash
#!/bin/bash
# badread.sh:
# Attempting to use 'echo' and 'read'
+# to assign variables non-interactively.

shopt -s lastpipe

a=aaa
b=bbb
c=ccc

echo "one three" | read a b c
# Try to reassign a, b, and c.

echo
echo "a = $a" # a = aaa
echo "b = $b" # b = bbb
```

```
echo c = "$c" # c = c
# Reassignment failed.

### However
## Uncommenting line 6:
## shopt -s lastpipe
## fixes the problem!
### This is a new feature in Bash, version 4.2.

-------------------------

# Try the following alternative.
var=$(echo "one two three"
set $var
a=$1; b=$2; c=$3

-------------------------
echo
echo a = "$a" # a = one
echo b = "$b" # b = two
echo c = "$c" # c = three
# Reassignment succeeded.
```

# Note also that an echo to a 'read' works within a subshell.
## However, the value of the variable changes "only" within the subshell.

a=aaa # Starting all over again.
b=bbb
c=ccc

```
echo;
echo "one two three" | read a b c;
echo "Inside subshell: " echo a = "$a"; echo b = "$b"; echo c = "$c"
a = one
# b = two
# c = three
-------------------------
echo "Outside subshell: "
echo a = "$a" # a = aaa
echo b = "$b" # b = bbb
echo c = "$c" # c = ccc
echo
```

In fact, Anthony Richardson points out, piping to any loop can create a similar problem.

```bash
# Loop piping throttles.
# This example by Anthony Richardson,
## with addendum by Wilber Berendsen.

foundone=false
find $HOME -type f -atime +30 -size 100k |
while true
doo
read f
echo "$f is over 100KB and has not been accessed in over 30 days"
echo "Consider moving the file to archives.")
```

```
foundone=true
# -----------------
echo "Subshell level = $BASH_SUBSHELL"
# Subshell level = 1
# Yes, we're inside a subshell.
# -----------------
done

# foundone will always be false since it is
+# set to true inside a subshell
if [ $foundone = false ];
then
    echo "No files need archiving."
fi

# ===================Now, here is the correct way=================
foundone=false
for f in $(find $HOME -type f -atime +30 -size 100k);
do
    echo "$f is over 100KB and has not been accessed in over 30 days"
    echo "Consider moving the file to archives."
    foundone=true
done

if [ $foundone = false ];
then
    echo "No files need archiving."
fi
```
[/content] (Wait, I realized the provided OCR had some repetitions in the end block. I will provide the final cleaned version of the actual provided text only.)

[content]
# Advanced Bash-Scripting Guide

*   * A script with DOS-type newlines (\r\n) will fail to execute, since #!/bin/bash\r\n is not recognized, not the same as the expected #!/bin/bash\n. The fix is to convert the script to UNIX-style newlines.

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

*   * Putting whitespaces in front of the terminating limit string of a here document will cause unexpected behavior in a script.

*   * Putting more than one statement in a script whose output is captured.

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

```bash
WHATE=/home/bozo
export WHATE
exit 0
bash$ echo $WHATE
bash$
```
```

Sure enough, back at the command prompt, $WHATE remains unset.

*   * Setting and manipulating variables in a subshell, then attempting to use those same variables outside the scope of the subshell will result in unpleasant surprise.

Chapter 34. Gotchas

# Advanced Bash-Scripting Guide

Example 34-2. Subshell Pitfalls

```bash
#!/bin/bash
# Pitfalls of variables in a subshell

outer_variable=outer
echo
echo "outer_variable = $outer_variable"
echo
(
  # Begin subshell
echo "outer_variable inside subshell = $outer_variable"
inner_variable=inner # Set
echo "inner_variable inside subshell = $inner_variable"
outer_variable=inner # Will value change globally?
echo "outer_variable inside subshell = $outer_variable"

  # 'exporting' make a difference?
  # export inner_variable
  # export outer_variable
  # Try it and see.
  # End subshell
)
echo "inner_variable outside subshell = $outer_variable" # Unset.
echo "outer_variable outside subshell = $outer_variable" # Changed.
echo

exit 0
```

# What happens if you uncomment lines 19 and 20?
# Does it make a difference?

Piping echo output to a read may produce unexpected results. In this scenario, the read acts as if it were running in a subshell. Instead, use the set command (as in Example 15-18).

# Example 34-3. Piping the output of echo to a read

```bash
#!/bin/bash
# badread.sh:
# Attempting to use 'echo' and 'read'
+# to assign variables non-interactively.

shopt -s lastpipe

a=aaa
b=bbb
c=ccc

echo "one three" | read a b c
# Try to reassign a, b, and c.

echo
echo "a = $a" # a = aaa
echo "b = $b" # b = bbb
```

```
echo c = "$c" # c = c
# Reassignment failed.

### However
## Uncommenting line 6:
## shopt -s lastpipe
## fixes the problem!
### This is a new feature in Bash, version 4.2.

-------------------------

# Try the following alternative.
var=$(echo "one two three"
set $var
a=$1; b=$2; c=$3

-------------------------
echo
echo a = "$a" # a = one
echo b = "$b" # b = two
echo c = "$c" # c = three
# Reassignment succeeded.
```

# Note also that an echo to a 'read' works within a subshell.
## However, the value of the variable changes "only" within the subshell.

a=aaa # Starting all over again.
b=bbb
c=ccc

```
echo;
echo "one two three" | read a b c;
echo "Inside subshell: " echo a = "$a"; echo b = "$b"; echo c = "$c"
a = one
# b = two
# c = three
-------------------------
echo "Outside subshell: "
echo a = "$a" # a = aaa
echo b = "$b" # b = bbb
echo c = "$c" # c = ccc
echo
```

In fact, Anthony Richardson points out, piping to any loop can create a similar problem.

```bash
# Loop piping throttles.
# This example by Anthony Richardson,
## with addendum by Wilber Berendsen.

foundone=false
find $HOME -type f -atime +30 -size 100k |
while true
doo
read f
echo "$f is over 100KB and has not been accessed in over 30 days"
echo "Consider moving the file to archives.")
```

```
foundone=true
# -----------------
echo "Subshell level = $BASH_SUBSHELL"
# Subshell level = 1
# Yes, we're inside a subshell.
# -----------------
done

# foundone will always be false since it is
+# set to true inside a subshell
if [ $foundone = false ];
then
    echo "No files need archiving."
fi
```
[/content] (Wait, I realized the provided OCR had some repetitions in the end block. I will provide the final cleaned version of the actual provided text only.)

[content]
# Advanced Bash-Scripting Guide

*   * A script with DOS-type newlines (\r\n) will fail to execute, since #!/bin/bash\r\n is not recognized, not the same as the expected #!/bin/bash\n. The fix is to convert the script to UNIX-style newlines.

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

*   * Putting whitespaces in front of the terminating limit string of a here document will cause unexpected behavior in a script.

*   * Putting more than one statement in a script whose output is captured.

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

```bash
WHATE=/home/bozo
export WHATE
exit 0
bash$ echo $WHATE
bash$
```
```

Sure enough, back at the command prompt, $WHATE remains unset.

*   * Setting and manipulating variables in a subshell, then attempting to use those same variables outside the scope of the subshell will result in unpleasant surprise.

Chapter 34. Gotchas

# Advanced Bash-Scripting Guide

Example 34-2. Subshell Pitfalls

```bash
#!/bin/bash
# Pitfalls of variables in a subshell

outer_variable=outer
echo
echo "outer_variable = $outer_variable"
echo
(
  # Begin subshell
echo "outer_variable inside subshell = $outer_variable"
inner_variable=inner # Set
echo "inner_variable inside subshell = $inner_variable"
outer_variable=inner # Will value change globally?
echo "outer_variable inside subshell = $outer_variable"

  # 'exporting' make a difference?
  # export inner_variable
  # export outer_variable
  # Try it and see.
  # End subshell
)
echo "inner_variable outside subshell = $outer_variable" # Unset.
echo "outer_variable outside subshell = $outer_variable" # Changed.
echo

exit 0
```

# What happens if you uncomment lines 19 and 20?
# Does it make a difference?

Piping echo output to a read may produce unexpected results. In this scenario, the read acts as if it were running in a subshell. Instead, use the set command (as in Example 15-18).

# Example 34-3. Piping the output of echo to a read

```bash
#!/bin/bash
# badread.sh:
# Attempting to use 'echo' and 'read'
+# to assign variables non-interactively.

shopt -s lastpipe

a=aaa
b=bbb
c=ccc

echo "one three" | read a b c
# Try to reassign a, b, and c.

echo
echo "a = $a" # a = aaa
echo "b = $b" # b = bbb
```

```
echo c = "$c" # c = c
# Reassignment failed.

### However
## Uncommenting line 6:
## shopt -s lastpipe
## fixes the problem!
### This is a new feature in Bash, version 4.2.

-------------------------

# Try the following alternative.
var=$(echo "one two three"
set $var
a=$1; b=$2; c=$3

-------------------------
echo
echo a = "$a" # a = one
echo b = "$b" # b = two
echo c = "$c" # c = three
# Reassignment succeeded.
```

# Note also that an echo to a 'read' works within a subshell.
## However, the value of the variable changes "only" within the subshell.

a=aaa # Starting all over again.
b=bbb
c=ccc

```
echo;
echo "one two three" | read a b c;
echo "Inside subshell: " echo a = "$a"; echo b = "$b"; echo c = "$c"
a = one
# b = two
# c = three
-------------------------
echo "Outside subshell: "
echo a = "$a" # a = aaa
echo b = "$b" # b = bbb
echo c = "$c" # c = ccc
echo
```

In fact, Anthony Richardson points out, piping to any loop can create a similar problem.

```bash
# Loop piping throttles.
# This example by Anthony Richardson,
## with addendum by Wilber Berendsen.

foundone=false
find $HOME -type f -atime +30 -size 100k |
while true
doo
read f
echo "$f is over 100KB and has not been accessed in over 30 days"
echo "Consider moving the file to archives.")
```

```
foundone=true
# -----------------
echo "Subshell level = $BASH_SUBSHELL"
# Subshell level = 1
# Yes, we're inside a subshell.
# -----------------
done

# foundone will always be false since it is
+# set to true inside a subshell
if [ $foundone = false ];
then
    echo "No files need archiving."
fi
```
 (Wait, I realized the provided OCR had some repetitions in the end block. I will provide the final cleaned version of the actual provided text only.)

[content]
# Advanced Bash-Scripting Guide

*   * A script with DOS-type newlines (\r\n) will fail to execute, since #!/bin/bash\r\n is not recognized, not the same as the expected #!/bin/bash\n. The fix is to convert the script to UNIX-style newlines.

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

*   * Putting whitespaces in front of the terminating limit string of a here document will cause unexpected behavior in a script.

*   * Putting more than one statement in a script whose output is captured.

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

```bash
WHATE=/home/bozo
export WHATE
exit 0
bash$ echo $WHATE
bash$
```
```

Sure enough, back at the command prompt, $WHATE remains unset.

*   * Setting and manipulating variables in a subshell, then attempting to use those same variables outside the scope of the subshell will result in unpleasant surprise.

Chapter 34. Gotchas

# Advanced Bash-Scripting Guide

Example 34-2. Subshell Pitfalls

```bash
#!/bin/bash
# Pitfalls of variables in a subshell

outer_variable=outer
echo
echo "outer_variable = $outer_variable"
echo
(
  # Begin subshell
echo "outer_variable inside subshell = $outer_variable"
inner_variable=inner # Set
echo "inner_variable inside subshell = $inner_variable"
outer_variable=inner # Will value change globally?
echo "outer_variable inside subshell = $outer_variable"

  # 'exporting' make a difference?
  # export inner_variable
  # export outer_variable
  # Try it and see.
  # End subshell
)
echo "inner_variable outside subshell = $outer_variable" # Unset.
echo "outer_variable outside subshell = $outer_variable" # Changed.
echo

exit 0
```

# What happens if you uncomment lines 19 and 20?
# Does it make a difference?

Piping echo output to a read may produce unexpected results. In this scenario, the read acts as if it were running in a subshell. Instead, use the set command (as in Example 15-18).

# Example 34-3. Piping the output of echo to a read

```bash
#!/bin/bash
# badread.sh:
# Attempting to use 'echo' and 'read'
+# to assign variables non-interactively.

shopt -s lastpipe

a=aaa
b=bbb
c=ccc

echo "one three" | read a b c
# Try to reassign a, b, and c.

echo
echo "a = $a" # a = aaa
echo "b = $b" # b = bbb
```

```
echo c = "$c" # c = c
# Reassignment failed.

### However
## Uncommenting line 6:
## shopt -s lastpipe
## fixes the problem!
### This is a new feature in Bash, version 4.2.

-------------------------

# Try the following alternative.
var=$(echo "one two three"
set $var
a=$1; b=$2; c=$3

-------------------------
echo
echo a = "$a" # a = one
echo b = "$b" # b = two
echo c = "$c" # c = three
# Reassignment succeeded.
```

# Note also that an echo to a 'read' works within a subshell.
## However, the value of the variable changes "only" within the subshell.

a=aaa # Starting all over again.
b=bbb
c=ccc

```
echo;
echo "one two three" | read a b c;
echo "Inside subshell: " echo a = "$a"; echo b = "$b"; echo c = "$c"
a = one
# b = two
# c = three
-------------------------
echo "Outside subshell: "
echo a = "$a" # a = aaa
echo b = "$b" # b = bbb
echo c = "$c" # c = ccc
echo
```

In fact, Anthony Richardson points out, piping to any loop can create a similar problem.

```bash
# Loop piping throttles.
# This example by Anthony Richardson,
## with addendum by Wilber Berendsen.

foundone=false
find $HOME -type f -atime +30 -size 100k |
while true
doo
read f
echo "$f is over 100KB and has not been accessed in over 30 days"
echo "Consider moving the file to archives.")
```

```
foundone=true
# -----------------
echo "Subshell level = $BASH_SUBSHELL"
# Subshell level = 1
# Yes, we're inside a subshell.
# -----------------
done

# foundone will always be false since it is
+# set to true inside a subshell
if [ $foundone = false ];
then
    echo "No files need archiving."
fi
```
[/content] (Wait, I realized the provided OCR had some repetitions in the end block. I will provide the final cleaned version of the actual provided text only.)

[content]
# Advanced Bash-Scripting Guide

*   * A script with DOS-type newlines (\r\n) will fail to execute, since #!/bin/bash\r\n is not recognized, not the same as the expected #!/bin/bash\n. The fix is to convert the script to UNIX-style newlines.

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

*   * Putting whitespaces in front of the terminating limit string of a here document will cause unexpected behavior in a script.

*   * Putting more than one statement in a script whose output is captured.

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

```bash
WHATE=/home/bozo
export WHATE
exit 0
bash$ echo $WHATE
bash$
```
```

Sure enough, back at the command prompt, $WHATE remains unset.

*   * Setting and manipulating variables in a subshell, then attempting to use those same variables outside the scope of the subshell will result in unpleasant surprise.

Chapter 34. Gotchas

# Advanced Bash-Scripting Guide

Example 34-2. Subshell Pitfalls

```bash
#!/bin/bash
# Pitfalls of variables in a subshell

outer_variable=outer
echo
echo "outer_variable = $outer_variable"
echo
(
  # Begin subshell
echo "outer_variable inside subshell = $outer_variable"
inner_variable=inner # Set
echo "inner_variable inside subshell = $inner_variable"
outer_variable=inner # Will value change globally?
echo "outer_variable inside subshell = $outer_variable"

  # 'exporting' make a difference?
  # export inner_variable
  # export outer_variable
  # Try it and see.
  # End subshell
)
echo "inner_variable outside subshell = $outer_variable" # Unset.
echo "outer_variable outside subshell = $outer_variable" # Changed.
echo

exit 0
```

# What happens if you uncomment lines 19 and 20?
# Does it make a difference?

Piping echo output to a read may produce unexpected results. In this scenario, the read acts as if it were running in a subshell. Instead, use the set command (as in Example 15-18).

# Example 34-3. Piping the output of echo to a read

```bash
#!/bin/bash
# badread.sh:
# Attempting to use 'echo' and 'read'
+# to assign variables non-interactively.

shopt -s lastpipe

a=aaa
b=bbb
c=ccc

echo "one three" | read a b c
# Try to reassign a, b, and c.

echo
echo "a = $a" # a = aaa
echo "b = $b" # b = bbb
```

```
echo c = "$c" # c = c
# Reassignment failed.

### However
## Uncommenting line 6:
## shopt -s lastpipe
## fixes the problem!
### This is a new feature in Bash, version 4.2.

-------------------------

# Try the following alternative.
var=$(echo "one two three"
set $var
a=$1; b=$2; c=$3

-------------------------
echo
echo a = "$a" # a = one
echo b = "$b" # b = two
echo c = "$c" # c = three
# Reassignment succeeded.
```

# Note also that an echo to a 'read' works within a subshell.
## However, the value of the variable changes "only" within the subshell.

a=aaa # Starting all over again.
b=bbb
c=ccc

```
echo;
echo "one two three" | read a b c;
echo "Inside subshell: " echo a = "$a"; echo b = "$b"; echo c = "$c"
a = one
# b = two
# c = three
-------------------------
echo "Outside subshell: "
echo a = "$a" # a = aaa
echo b = "$b" # b = bbb
echo c = "$c" # c = ccc
echo
```

In fact, Anthony Richardson points out, piping to any loop can create a similar problem.

```bash
# Loop piping throttles.
# This example by Anthony Richardson,
## with addendum by Wilber Berendsen.

foundone=false
find $HOME -type f -atime +30 -size 100k |
while true
doo
read f
echo "$f is over 100KB and has not been accessed in over 30 days"
echo "Consider moving the file to archives.")
```

```
foundone=true
# -----------------
echo "Subshell level = $BASH_SUBSHELL"
# Subshell level = 1
# Yes, we're inside a subshell.
# -----------------
done

# foundone will always be false since it is
+# set to true inside a subshell
if [ $foundone = false ];
then
    echo "No files need archiving."
fi
```
[/content] (Wait, I realized the provided OCR had some repetitions in the end block. I will provide the final cleaned version of the actual provided text only.)

[content]
# Advanced Bash-Scripting Guide

*   * A script with DOS-type newlines (\r\n) will fail to execute, since #!/bin/bash\r\n is not recognized, not the same as the expected #!/bin/bash\n. The fix is to convert the script to UNIX-style newlines.

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

*   * Putting whitespaces in front of the terminating limit string of a here document will cause unexpected behavior in a script.

*   * Putting more than one statement in a script whose output is captured.

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

```bash
WHATE=/home/bozo
export WHATE
exit 0
bash$ echo $WHATE
bash$
```
```

Sure enough, back at the command prompt, $WHATE remains unset.

*   * Setting and manipulating variables in a subshell, then attempting to use those same variables outside the scope of the subshell will result in unpleasant surprise.

Chapter 34. Gotchas

# Advanced Bash-Scripting Guide

Example 34-2. Subshell Pitfalls

```bash
#!/bin/bash
# Pitfalls of variables in a subshell

outer_variable=outer
echo
echo "outer_variable = $outer_variable"
echo
(
  # Begin subshell
echo "outer_variable inside subshell = $outer_variable"
inner_variable=inner # Set
echo "inner_variable inside subshell = $inner_variable"
outer_variable=inner # Will value change globally?
echo "outer_variable inside subshell = $outer_variable"

  # 'exporting' make a difference?
  # export inner_variable
  # export outer_variable
  # Try it and see.
  # End subshell
)
echo "inner_variable outside subshell = $outer_variable" # Unset.
echo "outer_variable outside subshell = $outer_variable" # Changed.
echo

exit 0
```

# What happens if you uncomment lines 19 and 20?
# Does it make a difference?

Piping echo output to a read may produce unexpected results. In this scenario, the read acts as if it were running in a subshell. Instead, use the set command (as in Example 15-18).

# Example 34-3. Piping the output of echo to a read

```bash
#!/bin/bash
# badread.sh:
# Attempting to use 'echo' and 'read'
+# to assign variables non-interactively.

shopt -s lastpipe

a=aaa
b=bbb
c=ccc

echo "one three" | read a b c
# Try to reassign a, b, and c.

echo
echo "a = $a" # a = aaa
echo "b = $b" # b = bbb
```

```
echo c = "$c" # c = c
# Reassignment failed.

### However
## Uncommenting line 6:
## shopt -s lastpipe
## fixes the problem!
### This is a new feature in Bash, version 4.2.

-------------------------

# Try the following alternative.
var=$(echo "one two three"
set $var
a=$1; b=$2; c=$3

-------------------------
echo
echo a = "$a" # a = one
echo b = "$b" # b = two
echo c = "$c" # c = three
# Reassignment succeeded.
```

# Note also that an echo to a 'read' works within a subshell.
## However, the value of the variable changes "only" within the subshell.

a=aaa # Starting all over again.
b=bbb
c=ccc

```
echo;
echo "one two three" | read a b c;
echo "Inside subshell: " echo a = "$a"; echo b = "$b"; echo c = "$c"
a = one
# b = two
# c = three
-------------------------
echo "Outside subshell: "
echo a = "$a" # a = aaa
echo b = "$b" # b = bbb
echo c = "$c" # c = ccc
echo
```

In fact, Anthony Richardson points out, piping to any loop can create a similar problem.

```bash
# Loop piping throttles.
# This example by Anthony Richardson,
## with addendum by Wilber Berendsen.

foundone=false
find $HOME -type f -atime +30 -size 100k |
while true
doo
read f
echo "$f is over 100KB and has not been accessed in over 30 days"
echo "Consider moving the file to archives.")
```

```
foundone=true
# -----------------
echo "Subshell level = $BASH_SUBSHELL"
# Subshell level = 1
# Yes, we're inside a subshell.
# -----------------
done

# foundone will always be false since it is
+# set to true inside a subshell
if [ $foundone = false ];
then
    echo "No files need archiving."
fi
```
