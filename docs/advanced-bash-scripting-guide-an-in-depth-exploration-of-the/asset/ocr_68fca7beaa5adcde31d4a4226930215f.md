# Advanced Bash-Scripting Guide

```
exit 0

# Output of function1:

# Within function1, $fclvar = 20.
# Within function2, $fclvar = 20.
```

This is documented in the Bash manual:

"Local can only be used within a function; it makes the variable name have a scope restricted to that function and its children." [emphasis added] The ABS Guide author considers this behavior to be a bug.

+   [111] Otherwise known as redundancy.
[112] Otherwise known as tautology.
[113] Otherwise known as a metaphor.
[114] Otherwise known as a recursive function.
[115] Too many levels of recursion may crash a script with a segfault.

```
#!/bin/bash

# Warning: Running this script could possibly lock up your system!
# If you're lucky, it will segfault before using all available memory.
recursive_function() {
  echo "$1" # Makes the function do something, and hastens the default.
  (( $1 < $2 )) && recursive_function $(( $1 + 1 )) $2;
  # As long as list parameter is less than 2nd,
  # increment and recurse.
}
recursive_function 1 50000 # Recurse 50000 levels!
# Most likely segfaults (depending on stack size, be limit by ulimit -m).
#n Recursion this deep might cause even a C program to segfault,
+# by using all the memory allotted to the stack.
```

```
echo "This will probably not print."
exit 0 # This script will not exit normally.
```

# Thanks, Stéphane Chazelas.

+   [116] as the first word of a command string. obvious alias is also meaningful at the beginning of a command.

+   [117] However, aliases do not expand positional parameters.

+   [118] The entries in /dev/null, /dev/zero, and /dev/urandom are virtual. These entries use very little drive space.

Some devices, such as /dev/null, /dev/zero, and /dev/urandom are virtual. They are not actual physical devices and exist only in software.
A block device reads and writes data in chunks, or blocks, in contrast to a character device, which accesses data in units. Examples of block devices are hard drives, CDROM drives, and flash drives. Examples of character devices are keyboards, modems, and sound cards.

+   [120]

Appendix T. ASCII Table