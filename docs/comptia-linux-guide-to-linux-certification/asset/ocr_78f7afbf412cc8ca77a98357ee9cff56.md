What here shall miss, our toil shall strive to mend.
[root@server1 ~]# 
You can also tell sed the specific lines to search by prefixing the search-and-replace expres-sion. For example, to force sed to replace the string “the” with “THE” globally on lines that contain the string “love,” you can use the following command:

```
[root@server1 ~]# cat prologue | sed /love/s//the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth the fatal loins of these two foes
A pair of star-cross'd lovers take THEIR life;
Whole misadventured piteous overthrows
Do with their death bury their parents' strife.
The fearful passage of THEIR death-mark'd love,
And the continuance of their parents' rage,
Which, but their children's end, nought could remove,
Is now the two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 ~]# 
You can also force sed to perform a search-and-replace on certain lines only. To replace the string “the” with “THE” globally on lines 5 to 8, you can use the following command:
```

```
[root@server1 ~]# cat prologue | sed 5,8s//the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth THE fatal loins of THESE two foes
A pair of star-cross'd lovers take THEIR life;
Whole misadventured piteous overthrows
Do with THEIR death bury THEIR parents' strife.
The fearful passage of their death-mark'd love,
And the continuance of their parents' rage,
Which, but their children's end, nought could remove,
Is now the two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 ~]# 
You can also use sed to remove unwanted lines of text. To delete all the lines that contain the word “the,” you can use the following command:
```

```
[root@server1 ~]# cat prologue | sed /the/d
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
```