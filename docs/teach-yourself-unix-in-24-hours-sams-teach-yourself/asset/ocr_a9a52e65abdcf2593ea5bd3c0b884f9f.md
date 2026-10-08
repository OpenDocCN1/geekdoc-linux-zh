3. There are two different ways you could have UNIX match all lines that contain the words not and cold: one uses grep and uses pipelines. Show both.

4. Use the -v flag with various grep commands, and show the command and pattern needed to match lines that:

```
Don't contain cabana
Don't contain either jazz or funk
Don't contain jazz, funk, disco, blues, or.
```

5. Use a combination of ts -l, cat -n and grep to find out the name of the 11th or 24th file in the /etc directory on your system.

6. There are two ways to look for lines containing any one of the words jazz, funk, disco, blues, and ska. Show both of them.

4. What does the following do?

```
sed "s/:*/ /;"" /etc/passwd | head
```

7. What does this one do?

```
sed "s/^$/ /" < testme
```

# Preview of the Next Hour

In the next hour, you are introduced to some more advanced pipelining commands and the incredibly powerful filter, awk.