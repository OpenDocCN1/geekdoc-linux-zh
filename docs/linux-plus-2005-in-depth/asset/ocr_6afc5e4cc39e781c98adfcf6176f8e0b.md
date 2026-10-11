[root@server1 root]# tr a A <prologue | sort | nl >newprologue
[root@server1 root]# cat newprologue

```
   1 And the contuinance of their parents' rAge.
   2 A pair of star-cross'd lovers take their life.
   3 Do with their death bury their parents' strife.
   4 From Ancient grudge break to new mutiny.
   5 From forth the fatal loins of these two foes
   6 In fair Verona, where we lay our scene,
   7 Is now the two hours' traffic of our stage;
   8 The fearful passage of their death-mark'd love,
   9 The which if you with patient ears attend,
  10 Two households, both alike in dignity,
  11 What here shall miss, our toil shall strive to mend.
  12 Where civil blood makes civil hands unclean.
  13 Which, but their children's end, nought could remove,
  14 Whole misadventured piteous overthrows
[root@server1 root]# _
```

Many Linux commands can be used to provide large amounts of useful text information. As a result, Linux administrators often use the sed and awk filter commands in conjunction with pipes to manipulate text information obtained from these commands.

The sed command is typically used to search for a certain string of text, and replaces that text string with another text string using the syntax s/search/replace/. For example, the following output demonstrates how sed can be used to search for the string “the” and replace it with the string “THE” in the prologue file used earlier:

```
[root@server1 root]# cat prologue | sed s/the/THE/
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth the fatal loins of these two foes
A pair of star-cross'd lovers take their life;
Whole misadventured piteous overthrows
Do with THEiR death bury their parents' strife.
The fearful passage of THEIR death-mark'd love,
And THE contuinance of their parents' rAge,
Which, but THEIR children's end, nought could remove,
Is now THE two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 root]# _
```