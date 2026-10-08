```
#
echo
done
echo
exit 0
```

The continue command, similar to break, optionally takes a parameter. A plain continue cuts short the current iteration within its loop and begins the next. A continue N terminates all remaining iterations at its loop level and continues with the next iteration, N levels above.

# Example 11-23. Continuing at a higher loop level

```
#!/bin/bash
# The "continue N" command, continuing at the Nth level loop.
for outer in I II III IV V # outer loop
do
  echo; -n "Group outer: "
#
for inner in 1 2 3 4 5 6 7 8 9 10 # inner loop
do
  if [ $inner -eq 4 && "$outer" = "III" ];
then
    continue 2 # Continue on loop on 2nd level, that is "outer loop".
    # Replace above line with a simple "continue"
    # to see normal loop behavior.
fi
echo -n "$inner " # 7 8 9 10 will not echo on "Group III."
done
#
```

done
echo; echo

# Exercise:
# Come up with a meaningful use for "continue N" in a script.
exit 0

# Example 11-24. Using continue N in an actual task

# Albert Reiner gives an example of how to use "continue N":
#

```
# Suppose I have a large number of jobs that need to be run, with
## any data that is to be treated in files of a given name pattern
## in a directory. There are several machines that access
## this directory, and I want to distribute the work over these
## different boxen.
# Then I use usually nohup something like the following on every box:
while true
```

Chapter 11. Loops and Branches