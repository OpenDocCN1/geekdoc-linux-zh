# 502 Lab : The read and printf Commands

Be sure you understand that the for statement assigns the values of a1, a2, and so forth to x, and it is those assignment operations that will be affected by the typeset command.

+   By examining the output of the second for statement, tell what the R6 does in the typeset command.

Answer:Your interaction should look like the following:

```
[11008]: a1=a a2=aa a3=aaa a4=aaaa a5=aaaaa
[11009]: for x in $s1 $s2 $s3 $s4 $s5 ; do print "$x"; done
a aa aaa aaaa aaaaaa
```

```
[11010]: typeset -R6 x
[11011]: for x in $s1 $s2 $s3 $s4 $s5 ; do print "$x"; done
a aa aaa aaaa aaaaa
```

[11012]:

The second loop prints the values right-justified in fields that are six characters wide. The default behavior is to left-justify the values.

> Note the quotes around $x in the print command. Without them, the spaces causing the output to be right-justified would be lost.

![](bbox=[0.12635, 0.631, 0.22638, 0.703])

> You can put a space between the R and the 6 in the typeset command, which might make your code easier to read.

![](bbox=[0.12635, 0.715, 0.22638, 0.787])

+   What happens if the width of x is too small to hold a value assigned to it?

Answer:The answer is truncated, as the following interaction shows:

```
[11012]: typeset -R3 x
```