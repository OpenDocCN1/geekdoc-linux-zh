
The following is a summary of the **sort** command.

**sort** - Sort lines of files (alphabetically by default).

Options:
- **-b** Ignore leading spaces and tabs.
- **-c** Check whether files are already sorted, and if so, do nothing.
- **-d** Ignore punctuation and sort in dictionary order.
- **-f** Ignore the case of entries when sorting.
- **-i** Ignore non-ASCII characters when sorting.
- **-ks** Use field *s* as the field on which to base the sort.
- **-m** Merge sorted files.
- **-n** Sort in numeric order.
- **-o file** Specify the output file name rather than write to standard output.
- **-r** Reverse the order of the sort by starting with the last letter of the alphabet or with the largest number, as we did in the example.
- **+n** Skip *n* fields or columns before sorting.

## **cmp, diff, and comm**

A fact of life is that as you go about editing files, you may occasionally lose track of what changes you have made to which files. You may then need to make comparisons of files. Let's take a look at three such commands, **cmp**, **diff** and **comm** and see how they compare files.

Let's assume that we have modified a script called **llsum**. The unmodified version of **llsum** was saved as **llsum.orig**. Using the **head** command we can view the first 20 lines of **llsum** and then the first 20 lines of **llsum.orig**:

![](img/75f39fc91296b889c0653851accdfd46_651_0.png)

```text
# head -20 llsum
#
#!/bin/sh
# Displays a truncated long listing (ll) and
# displays size statistics
# of the files in the listing.

ll $* | \
awk ' BEGIN { x=i=0; printf "%-25s%-10s%8s%8s\n",
"FILENAME", "OWNER", "SIZE", "TYPE" }
$1 ~ /^[-dlps]/ { # line format for normal files
printf "%-25s%-10s%8d", $9, $3, $5
x = x + $5
i++
}
$1 ~ /^\-/ { printf "%8s\n", "file" } # standard file
types
$1 ~ /^d/ { printf "%8s\n", "dir" }
$1 ~ /^l/ { printf "%8s\n", "link" }
$1 ~ /^p/ { printf "%8s\n", "pipe" }
$1 ~ /^s/ { printf "%8s\n", "socket" }
$1 ~ /^(bc)/ { # line format for device files
printf "%-25s%-10s%8s%8s\n", $10, $3, "", "dev"
}
#
```

```text
# head -20 llsum.orig
#
#!/bin/sh
# Displays a truncated long listing (ll) and
# displays size statistics
# of the files in the listing.

ll $* | \
awk ' BEGIN { x=i=0; printf "%-16s%-10s%8s%8s\n",
"FILENAME", "OWNER", "SIZE", "TYPE" }
$1 ~ /^[-dlps]/ { # line format for normal files
printf "%-16s%-10s%8d", $9, $3, $5
x = x + $5
i++
}
$1 ~ /^\-/ { printf "%8s\n", "file" } # standard file
types
$1 ~ /^d/ { printf "%8s\n", "dir" }
$1 ~ /^l/ { printf "%8s\n", "link" }
$1 ~ /^p/ { printf "%8s\n", "pipe" }
$1 ~ /^s/ { printf "%8s\n", "socket" }
$1 ~ /^(bc)/ { # line format for device files
printf "%-16s%-10s%8s%8s\n", $10, $3, "", "dev"
}
```

I'm not sure what changes I made to **llsum.orig** to improve it, so we can first use **cmp** to see whether indeed differences exist between the files.

```text
$
$ cmp llsum llsum.orig
llsum llsum.orig differ: char 154, line 6
$
```

**cmp** does not report back much information, only that character 154 in the file at line 6 is different in the two files. There may indeed be other differences, but this is all we know about so far.

To get information about all of the differences in the two files we could use the **-l** option to **cmp**:

```text
$ cmp -l llsum llsum.orig
   154 62  61
   155 65  66
   306 62  61
   307 65  66
   675 62  61
   676 65  66
```

This is not all that useful an output to me. I want to see not only the position of the differences, but also the differences themselves.

Now we can use **diff** to describe all the differences in the two files:

```text
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
---
>	printf "%-16s%-10s%s%s\n",$10,$3,"","dev"
$
```

![](img/75f39fc91296b889c0653851accdfd46_652_0.png)

![](img/75f39fc91296b889c0653851accdfd46_652_1.png)

We now know that lines 6, 9, and 25 are different in the two files and these lines are also listed for us. From this listing, we can see that the number 16 in **llsum.orig** was changed to 25 in the newer **llsum** file, and this accounts for all of the differences in the two files. The less than sign (<) precedes lines from the first file, in this case **llsum**. The greater than sign (>) precedes lines from the second file, in this case **llsum.orig**. I made this change, starting the second group of information from character 16 to character 25, because I wanted the second group of information, produced by **llsum**, to start at column 25. The second group of information is the *owner*, as shown in the following example:

```text
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
sam_adduser          denise       1010    file
tdoIan               denise       1024    dir
trash                denise       4554    file
trash.out            denise        329     file
typescript           denise       2017    file

The files listed occupy 393605 bytes (0.3754 Mbytes)
Average file size is 13120 bytes
```

When we run **llsum.orig**, clearly the second group of information, which is the owner, starts at column 16 and not column 25:

```text
$ llsum.orig
FILENAME          OWNER      SIZE     TYPE

README            denise     810      file
backup_files      denise     3408     file
biography         denise     427      file
cshtest           denise     1024     dir
gkill             denise     1855     file
gkill.out         denise     191      file
hostck            denise     924      file
ifstat            denise     1422     file
ifstat.int        denise     2147     file
ifstat.out        denise     723      file
introdos          denise     54018    file
introux           denise     52476    file
letter            denise     23552    file
letter.auto       denise     69632    file
letter.auto.rec   denise     71680    file
letter.backup     denise     23552    file
letter.1ck        denise     57       file
letter.recover    denise     69632    file
llsum             denise     1267     file
llsum.orig        denise     1267     file
llsum.out         denise     1657     file
llsum.tomd.out    denise     1356     file
psg               denise     670      file
psg.int           denise     802      file
psg.out           denise     122      file
sam_adduser       denise     1010     file
tdoIan            denise     1024     dir
trash             denise     4554     file
trash.out         denise     329      file
typescript        denise     3894     file

The files listed occupy 395482 bytes (0.3772 Mbytes)
Average file size is 13182 bytes
script done on Mon Dec 11 12:59:18
$
```

![](img/75f39fc91296b889c0653851accdfd46_655_0.png)

We can compare two sorted files using **comm** and see the lines that are unique to each file, as well as the lines found in both files. When we compare two files with **comm**, the lines that are unique to the first file appear in the first column, the lines unique to the second file appear in the second column and the lines contained in both files appear in the third column. Let’s go back to the */etc/passwd* file to illustrate this comparison. We’ll compare two */etc/passwd* files, the active */etc/passwd* file in use and an old */etc/passwd* file from a backup:

```text
# comm /etc/passwd /etc/passwd.backup

				root:PygQCCkVH65hyQ:0:0:root:/root:/bin/bash
				bin:*:1:1:bin:/bin:
				daemon:*:2:2:daemon:/sbin:
				adm:*:3:4:adm:/var/adm:
				lp:*:4:7:lp:/var/spool/lpd:
				sync:*:5:0:sync:/sbin:/bin/sync
				shutdown:*:6:11:shutdown:/sbin:/sbin/shutdown
				halt:*:7:0:halt:/sbin:/sbin/halt
				mail:*:8:12:mail:/var/spool/mail:
				news:*:9:13:news:/var/spool/news:
				uucp:*:10:14:uucp:/var/spool/uucp:
				operator1:*:12:0:operator:/root:
				operator:*:11:0:operator:/root:
				games:*:12:100:games:/usr/games:
				gopher:*:13:30:gopher:/usr/lib/gopher-data:
				ftp:*:14:50:FTP User:/home/ftp:
				man:*:15:15:Manuals Owner://
				nobody:*:65534:65534:Nobody://bin/false
				col:Wh0yzfAV2qm2Y:100:100:Caldera
				OpenLinux User:/home/col:/bin/bash
```
