# Advanced Bash-Scripting Guide

Example 21-3. Running parallel processes in subshells

```
(cat list1 list2 list3 | sort | uniq > list123) &
(cat list4 list5 list6 | sort | uniq > list456) &
# Merges and sorts both sets of lists simultaneously.
# Running in background ensures parallel execution.
#
# Same effect as
# cat list1 list2 list3 | sort | uniq > list123 &
# cat list4 list5 list6 | sort | uniq > list456 &

wait # Don't execute the next command until subshells finish.

diff list123 list456
```

Redirecting I/O to a subshell uses the "| pipe operator, in ls -al (command).

> A code block between curly brackets does not launch a subshell.

```
{ command1; command2; command3;...commandN; }

var1=23
echo "$var1" # 23

var1=76;
echo "$var1" # 76
```