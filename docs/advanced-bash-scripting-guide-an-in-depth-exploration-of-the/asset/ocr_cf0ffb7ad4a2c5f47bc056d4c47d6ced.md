# Advanced Bash-Scripting Guide

```
## but an entire script?
# If you need something really elegant...
# consider writing the application in C or C++
# using appropriate library functions, such as 'alarm' and 'setimer.'
exit 0
```

An alternative is using stty.

# Example 9-3. Once, more timed input

```
#!/bin/bash
# timeout.sh

# Written by Stephane Chazelas,
# and modified by the document author.

INTERVAL=5 # timeout interval

timed_read() {
timeout=$1
varname=$2
old_tty_settings='stty -g'
stty -icanon 0 time $(timeout)0
eval read $varname # or just read $varname
stty "$old_tty_settings"
# See page for "stty."
}
```

echo; echo -n "What's your name? Quick!"
timed_read $INTERVAL $your_name

+   # This may not work on every terminal type.
# The maximum timeout depends on the terminal.
+# (it is often 25.5 seconds).

```
echo
if [ -z "$yourname" ]; # If name input before timeout
then
echo "Your name is $yourname."
else
echo "Timed out."
fi
e
```

```
# The behavior of this script differs somewhat from "timed-input.sh."
# At each keystroke, the counter resets.
exit 0
```

Perhaps the simplest method is using the -t option to read.

# Example 9-4. Timed read

```
#!/bin/bash
```

Chapter 9. Another Look at Variables