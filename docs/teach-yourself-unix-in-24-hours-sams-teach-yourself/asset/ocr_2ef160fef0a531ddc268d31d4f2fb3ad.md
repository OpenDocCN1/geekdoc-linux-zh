One more slight modification and it's:

```
% ls -l | awk '{ totalsize += $4 } END { print "You have a\ntotal-of \"totalize" bytes used in files." }'
You have a total of 29249 bytes used in files.
```

9. Here's another addition that can make this program even more fun:

```
% ls -l | awk '{ totalsize += $5 } END { print "You have a\ntotal-of \"totalize" bytes used across "NR" files." }'
You have a total of 29249 bytes used across 11 files.
```

An easy way to see all this is to create an awk program file:

```
cat << EOF > script
{ totalsize += $4 }
END { print "You have a total of \"totalsize\" bytes used across \"NR\ files." }
EOF
```

% ls -l | awk -f script
You have a total of 29249 bytes used across 11 files.

10. Here's one last example before I leave. Scripts in awk are really programs and can do within the flow-control capabilities you want (and then some!). One thing you can do within an awk script is to have conditional execution of scripts, the if-condition. The length function returns the number of characters in the argument:

```
% awk -F: '{ if (length($1) == 2) print $0 }' /etc/passwd | wc -l 26
```

Can you tell what this does? First off, notice that it uses the /etc/passwd file for input and a colon as the field delimiter (-F:). For each line in the password file, this awk script tests to see whether the length of the first field (the account name) is exactly two characters. If it is, the entire line from the password file is printed. All lines are printed by the we program, because I used -l reports the total number of lines read.

What this command tells us is that on the machine, there are 26 accounts for which the account name is two characters long.

11. The next logical question is, "How many accounts name have a length of each possible number of characters?" To find out, I'll use an advanced feature of awk to utilize: I will have the program build a table to keep track of the count, with one entry per number of characters in the name:

```
cat << EOF > script
{ count[length($1)]++ }
END {
 for (i=1; i < 9; i++) print "There are " count[i] " accounts with " i " letter names."\ }
EOF
```

![](bbox=[0.075, 0.885, 0.145, 0.955])