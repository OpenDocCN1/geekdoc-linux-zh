# Advanced Bash-Scripting Guide

```
# It is now ready to process its 2nd line (which is also numbered '$' as
# it's the last one).
# It sees is not matched by any <range>, so its job is done.

# In few word this sed command:
# "On the first line delete, remove any character up to the right-most space,
# then print it."

# A better way to do this would have been:
# sed -e 's/.*/ //q'

# Here, two <range>-action's (could have been written)
# sed -e 's/.*/ // -e q:

# range               action
# nothing (matches line)  s/. //
# nothing (matches line)  q (quit)

# Here, sel reads its first line of input.
# It performs both actions, and prints the line (substituted) before
#+ quitting (because of the "q" action) since the "-n" option is not passed.
# ==================================================================
# An even simpler alteative to the above one-line script would be:
# head -c4 /var/rundiram/ od -An -tu4

exit
```

See [Example 16-39].

lists the (tail) end of a file to stdout. The default is 10 lines, but this can be changed with the -n
option. Commonly used to keep track of changes to a system logfile, using the -f option, and
outputs lines appended to the file.

# Example 16-15. Using tail to monitor the system log

```
#!/bin/bash

filename=sys.log

cat /dev/null > $filename; echo "Creating / cleaning out file"
# Creates the file if it does not already exist,
+# and truncates it to zero length if it does.
# > filename and filename also work.

tail /var/log/messages > $filename
# /var/log/messages must have world read permission for this to work.

echo $filename contains tail end of system log.

ext 0
```

+   - To list specific lines of a text file, pipe the output of head to tail -n 1. For example head -n 8 database.txt | tail -n 1 lists the 8th line of the file database.txt.

To set a variable to a given block of a text file:

Chapter 16. External Filters, Programs and Commands

241