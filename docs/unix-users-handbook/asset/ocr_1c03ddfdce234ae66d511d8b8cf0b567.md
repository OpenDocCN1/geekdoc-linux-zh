I'm not sure what changes I made to **llsum.orig** to improve it, so we can first use **cmp** to see whether indeed differences exist between the files.

```
$
$ cmp llsum llsum.orig
llsum llsum.orig differ: char 154, line 6
$
```

**cmp** does not report back much information, only that character 154 in the file at line 6 is different in the two files. There may indeed be other differences, but this is all we know about so far.

To get information about all of the differences in the two files we could use the **-l** option to **cmp**:

```
$ cmp -l llsum llsum.orig
   154 62  61
   155 65  66
   306 62  61
   307 65  66
   675 62  61
   676 65  66
```

This is not all that useful an output to me. I want to see not only the position of the differences, but also he differences themselves.

Now we can use **diff** to describe all the differences in the two files:

```
$ diff llsum llsum.orig
6c6
< awk ' BEGIN { x=i=0; printf "%-25s%-10s%s%s%s\n", \
---
> awk ' BEGIN { x=i=0; printf "%-16s%-10s%s%s%s\n", \
9c9
<                    printf "%-25s%-10s%8d",$9,$3,$5
---
>                    printf "%-16s%-10s%8d",$9,$3,$5
19c19
<                    printf "%-25s%-10s%s%s%s\n",$10,$3,"","dev"
```

![](bbox=[0.87, 0.16, 0.97, 0.27])

![](bbox=[0.87, 0.59, 0.97, 0.7])