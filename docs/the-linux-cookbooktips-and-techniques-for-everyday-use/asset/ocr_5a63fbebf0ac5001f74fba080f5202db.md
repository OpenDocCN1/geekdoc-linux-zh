# The Linux Cookbook: Tips and Techniques for Everyday Use:

+   • To check out revision 1.14 of file `novel', type:

```
$ co -l -r1.14 novel RET
```

*NOTE:* Before checking out an old revision of a file, remember to check in the latest changes first, or they may be lost.

[ < ] [ > ] [ << ] [ Up ] [ >> ] [Top] [Contents] [Index] [ ? ]

# 9.7.3 Viewing a File's Revision Log

Use rlog to view the RCS revision log for a file—type rlog followed by the name of a file to list all of the revisions of that file.

+   • To view the revision log for file `novel', type:

```
$ rlog novel RET
RCS file: novel,v
Working file: novel
head: 1.2
branch:
locks: strict
access list:
symbolic names:
keyword substitution: kv
total revisions: 2;      selected revisions: 2
description:
The Great American Novel.
----------------------------------------
revision 1.2
date: 1991/06/20 15:31:44;  author: leo;  state: Exp;  lines: +2 -2
Second draft.
----------------------------------------
revision 1.1
date: 1991/06/21 19:03:58;  author: leo;  state: Exp;
Initial revision
============================================================
$
```

This command outputs the revision log for the file `novel'; it lists information about the RCS repository, including its name (`novel,v') and the name of the actual file (`novel'). It also shows that there are two revisions—the first, which was checked in to RCS on 20 June 1991, and the second, which was checked in to RCS the next day, on 21 June 1991.

[ < ] [ > ] [ << ] [ Up ] [ >> ] [Top] [Contents] [Index] [ ? ]