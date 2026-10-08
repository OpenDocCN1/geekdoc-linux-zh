```
---
>	printf "%-16s%-10s%s%s\n",$10,$3,"","dev"
$

```

We now know that lines 6, 9, and 25 are different in the two files and these lines are also listed for us. From this listing, we can see that the number 16 in **llsum.orig** was changed to 25 in the newer **llsum** file, and this accounts for all of the differences in the two files. The less than sign (<) precedes lines from the first file, in this case **llsum**. The greater than sign (>) precedes lines from the second file, in this case **llsum.orig**. I made this change, starting the second group of information from character 16 to character 25, because I wanted the second group of information, produced by **llsum**, to start at column 25. The second group of information is the *owner*, as shown in the following example:

```
$ llsum
FILENAME              OWNER         SIZE    TYPE

README                denise        810     file
backup_files          denise        3408    file
biography             denise        427     file
cshtest              denise       1024     dir
gkill                denise       1855    file
gkill.out            denise        191     file
hostck               denise        924     file
ifstat               denise       1422    file
ifstat.int           denise       2147    file
ifstat.out           denise        723     file
introdos             denise      54018    file
introux              denise      52476    file
letter               denise      23552    file
letter.auto          denise      69632    file
letter.auto.recover  denise      71680    file
letter.backup        denise      23552    file
letter.lck           denise         57     file
letter.recover       denise      69632    file
llsum                denise       1267    file
llsum.orig           denise       1267    file
llsum.out            denise       1657    file
llsum.tomd.out       denise       1356    file
psg                  denise        670     file
psg.int              denise        802     file
psg.out              denise        122     file
```