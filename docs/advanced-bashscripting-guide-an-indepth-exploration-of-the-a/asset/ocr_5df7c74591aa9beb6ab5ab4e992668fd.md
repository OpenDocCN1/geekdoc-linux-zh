# Advanced Bash–Scripting Guide

speeds things up a bit.

**agrep** extends the capabilities of **grep** to approximate matching. The search string may differ by a specified number of characters from the resulting matches. This utility is not part of the core Linux distribution.

![](bbox=[0.268, 0.197, 0.298, 0.222])

To search compressed files, use **zgrep**, **zegrep**, or **zfgrep**. These also work on non-compressed files, though slower than plain **grep**, **egrep**, **fgrep**. They are handy for searching through a mixed set of files, some not.

To search **bzipped** files, use **bgrep**.

look

The command **look** works like **grep**, but does a lookup on a "dictionary", a sorted list. By default, **look** searches for a match in `/usr/dict/words`, but a different dictionary file may be specified.

# Example 12–13. Checking words in a list for validity

```
#!/bin/bash
# look: Does a dictionary lookup on each word in a data file.
file=words.data # Data file from which to read words to test.
echo
while [ "$Word" != end ] # Last word in data file.
do
read word $? > /dev/null # Don't display lines in dictionary file.
lookup=$? # Exit status of 'look' command.

if [ "$lookup" -eq 0 ];
then
necho "\$word\" is valid.
else
necho "\$word\" is invalid.
fi

done <"$file" # Redirects stdin to $file, so "reads" come from there.
echo
exit 0
------------------------------------------------------------
# Code below line will not execute because of "exit" command.
```

Stephane Chaselas proposes the following, more concise alternative:

```
while read word && [[ $word != end ]]
```

# 12.4. Text Processing Commands