# Advanced Bash-Scripting Guide

OR logical operator. In a test construct, the || operator causes a return of 0 (success) if either the linked test conditions are true.

Run job in background. A command followed by an & will run in the background.

```
bash$ sleep 10 &
[1] 850
[1]+ sleep 10
```

Within a script, commands and even loops run in the background.

# Example 3-3. Running a loop in the background

```
#!/bin/bash
# background-loop.sh

for i in 1 2 3 4 5 6 7 8 9 10\    # First loop.
  echo -n "$i" 
  done & # Run this in background after second loop.
       # Will sometimes execute second loop.

echo    # This 'echo' sometimes will not display.

for i in 11 12 13 14 15 16 17 18 19 20 # Second loop.
do
  echo -n "$i"
  done

echo    # This 'echo' sometimes will not display.

=======================================================================
# The expected output from the script:
# 1 2 3 4 5 6 7 8 9 10
# 11 12 13 14 15 16 17 18 19 20
# do

# Sometimes, though, you get:
# 11 12 13 14 15 16 17 18 19 20
# 1 2 3 4 5 6 7 8 9 10 bozo $
# (The second 'echo' doesn't execute. Why?)

# Occasionally also:
# 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
# (The first 'echo' doesn't execute. Why?)

# Very rarely something like:
# 11 12 13 1 2 3 4 5 6 7 8 9 10 14 15 16 17 18 19 20
# The foreground loop preempts the background one.
```

```
exit 0

# Nasimuddin Ansari suggests adding sleep 1
#+ after the echo -n "$i" in lines 6 and 14,
#+ for some real fun.
```

Chapter 3. Special Characters