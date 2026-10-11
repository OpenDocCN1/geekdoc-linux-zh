
The `$Date$` value appears in UTC or Universal Coordinated Time format, formerly known as Greenwich Mean Time. The symbolic name that `$Name$` represents is an alias that you can use to refer to a particular revision. To associate a symbolic name with a specific revision number, use the `-n<name>` switch when checking in a file. The `$State$` field defaults to experimental (Exp) because RCS considers all check-ins to be trial runs until they are specifically marked as stable (Stab) or released (Rel) using the `-s<state>` switch.

## The ident Command

The `ident` command locates RCS keywords in files of all types and displays them to standard output. This feature lets you find out which revisions of which modules are used in a given program release. `ident` works by extracting strings of the form `$KEYWORD: VALUE $` from source, object, and binary files. It even works on raw binary data files and core dumps. In fact, because `ident` looks for any instance of the `$KEYWORD: VALUE $` pattern, you can also use words that are not RCS keywords.

This enables you to embed additional information into programs, for example, a company name. Embedded information can be a valuable tool for isolating problems to a specific code module. The slick part of this feature is that RCS updates the identification strings automatically—a real bonus for programmers and project managers.

### Example

![](img/be588b36b489136ce784030a08a1d3d4_456_0.png)

To illustrate using `ident`, create the following source file, check it in (using `-u`), compile and link it, ignore the warning you might get that `rcsid` is defined but not used, and then run the `ident` command on it.

```c
/*
 * $Id$
 * prnenv.c - Display values of environment variables.
 */
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

static char rcsid[] = "$ Id $\n";

int main(void)
{
    extern char **environ;
    char **my_env = environ;
    while(*my_env) 
       printf("%s\n", *my_env++);
    return EXIT_SUCCESS;
}
```

### Output

```bash
$ gcc prnenv.c -o prnenv
$ ident prnenv
prnenv:
   $ Id: prnenv.c,v 1.1 1999/07/20  05:57:59  kwall  Exp  $
```

The statement `static char rcsid[] = "$ Id \n";` takes advantage of RCS's keyword expansion to create a static text buffer that holds the value of the `$ Id $` keyword in the compiled program that `ident` can extract.

What happened? The `$ Id $` keyword expanded as previously described and `gcc` compiled the expanded text into the binary. To confirm this, page through the source code file and compare the `$ Id $` string in the source code to `ident`'s output. The two strings match exactly.

## Using rcsdiff

If you need to see the differences between your modified working file and its pristine counterpart in the repository, use the `rcsdiff` command. `rcsdiff` compares file revisions. In its simplest form, `rcsdiff filename`, `rcsdiff` compares the latest revision of `filename` in the repository with the working copy of `filename`. You can compare specific revisions using the `-r` option. The general format for comparing specific file revisions using `rcsdiff` is as follows:

```
rcsdiff [ -rfIes [ -rfIe2 ] ] filename
```

> **TIP**
>
> The `diff(1)` command is much more powerful and generalized than `rcsdiff`. `rcsdiff` is meant only for use with RCS. If you need to compare two (or more) text files, use the `diff` command.

### Examples

#### Example

1. For basic `rcsdiff` use, consider the sample program `prnenv.c`. Check out a locked version of it and remove the static char buffer. The result should closely resemble the following:

```c
/*
 * $Id: prnenv.c,v 1.1 1999/07/20  05:22:42  kwall  Exp  kwall $
 * prnenv.c - Display values of environment variables.
*/
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(void)
{
    extern char **environ;
    char **my_env = environ;
    while(*my_env)
        printf("%s\n", *my_env++);
    return EXIT_SUCCESS;
}
```

![](img/be588b36b489136ce784030a08a1d3d4_458_0.png)

#### Output

```bash
$ rcsdiff prnenv.c
=====
RCS file: RCS/prnenv.c,v
retrieving revision 1.1
diff -rl.1 prnenv.c
9d8
< static char rcsid[] = "$ Id: prnenv.c,v 1.1 \
1999/07/20 05:57:59 kwall Exp
kwall $\n";
```

This output means that line **9** in revision 1.1 would have appeared on line 8 of `prnenv.c` if it had not been deleted.

![](img/be588b36b489136ce784030a08a1d3d4_458_1.png)

#### Example

2. To compare specific revisions to each other using the `-r` option, check `prnenv.c` into the repository, check it right back out with a lock, add a `sleep(5)` statement immediately above `return`, and, finally, check this third revision back in with the `-u` option. You should now have three revisions of `prnenv.c` in the repository. First, compare revision 1.1 to the working file:

```bash
$ rcsdiff -r1.1 prnenv.c
2c2
< * $ Id: prnenv.c,v 1.1 1999/07/20 05:57:59 kwall Exp $
--
> * $ Id: prnenv.c,v 1.2 1999/07/20 06:00:47 kwall Exp $
9d8
< static char rcsid[] = "$ Id: prnenv.c,v 1.1 1999/07/20 05:57:59 kwall
Exp $\n";
17a17
<
---
>
sleep(5);
```

Next, compare revision 1.2 to revision 1.3:

```bash
$ rcsdiff -r1.2 -r1.3 prnenv.c
==========================================================
RCS file: RCS/prnenv.c,v
retrieving revision 1.2
retrieving revision 1.3
diff -r1.2 -r1.3
2c2
< * $Id: prnenv.c,v 1.2 1999/07/20 06:00:04 kwall Exp $
---
> * $ Id: prnenv.c,v 1.3 1999/07/20 06:00:47 kwall Exp $
16a17
>
sleep(5);
```

`rcsdiff` is a useful utility for viewing changes to RCS files or for preparing to merge multiple revisions into a single revision.

## Other RCS Commands

Besides `ci`, `co`, `ident`, and `rcsdiff`, the RCS suite includes `rlog`, `rcsclean`, and, of course, `rcs`. These additional commands extend your control of your source code by allowing you to merge or delete RCS files, review log entries, and perform other administrative functions.

## Using rcsclean

`rcsclean` does what its name suggests: It cleans up RCS working files. The basic syntax is `rcsclean [options] [file . . . ]`. A bare `rcsclean` command will delete all working files unchanged since they were checked out. The `-u` option tells `rcsclean` to unlock any locked files and remove unchanged working files. You can specify a revision to delete using the `-rM.N` format. For example, the following command removes the 2.3 revision of `foobar.c`:

```bash
$ rcsclean -r2.3 foobar.c
```

### Example

![](img/be588b36b489136ce784030a08a1d3d4_460_0.png)

### Example

The following command removes an unlocked, unchanged revision of `prnenv.c`:

```bash
$ co -u -r1.1 prnenv.c
RCS/prnenv.c prnenv.c
revision 1.1 (unlocked)
```

![](img/be588b36b489136ce784030a08a1d3d4_460_1.png)

### Output

```bash
done
$ rcsclean -r1.1 prnenv.c
rm -f prnenv.c
```

The first command checked out an unlocked version of `prnenv.c` in order to have a version to work with. The second command promptly cleaned it up (that is, deleted it).

## Using rlog

`rlog` prints the log messages and other information about files stored in the RCS repository. The `-R` option tells `rlog` to display only filenames. To see a list of all the files in the repository, for example, `rlog -R RCS/*` is the proper command (of course, you could always type `ls -1 RCS`, too). If you want to see a list of only the locked files, use the `-L` option. To see the log information on all files locked by the user named Gomer, use the `-l` option.

### Example

![](img/be588b36b489136ce784030a08a1d3d4_460_2.png)

### Example

This example displays all log information for all revisions of `prnenv.c`:

![](img/be588b36b489136ce784030a08a1d3d4_460_3.png)

### Output

```bash
$ rlog prnenv.c

RCS file: RCS/prnenv.c,v
Working file: prnenv.c
head: 1.3
branch:
locks: strict
access list:
symbolic names:
keyword substitution: kv
total revisions: 3; selected revisions: 3
description:
ew

--------------------------

revision 1.3
date: 1999/07/20 06:00:47; author: kwall; state: Exp; lines: +2 -1
added sleep

revision 1.2
date: 1999/07/20 06:00:04; author: kwall; state: Exp; lines: +1 -2
deleted buffer

revision 1.1
date: 1999/07/20 05:57:59; author: kwall; state: Exp;
Initial revision
```

## Using rcs

The `rcs` command is primarily an administrative command. In normal usage, though, it is useful in two ways. If you checked out a file as read-only, and then made changes you can't bear to lose, `rcs -l filename` will check out `filename` with a lock without simultaneously overwriting the working file. If you need to break a lock on a file checked out by someone else, `rcs -u filename` is the command to use. The file is unlocked, and a message is sent to the original locker containing an explanation from you about why you broke the lock.

Recall that each time you check a file in, you can type a check-in message explaining what has changed or what you did. If you make a typographical error or some other mistake in the check-in message, or would simply like to add additional information to it, you can use the following `rcs` command:

```bash
$ rcs -mrev:msg
```

`rev` is the revision whose message you want to correct or modify and `msg` is the corrected or additional information you want to add.

### Example

![](img/be588b36b489136ce784030a08a1d3d4_462_0.png)

### Example

This example uses `rcs` to change the check-in message for revision 1.2 of `prnenv.c`:

```bash
$ rcs -m1.2:"Deleted static buffer 'rcsid[]'" prnenv.c
RCS file: RCS/prnenv.c,v
done
```

![](img/be588b36b489136ce784030a08a1d3d4_462_1.png)

### Output

```bash
$ rlog -r1.2 prnenv.c
RCS file: RCS/prnenv.c,v
Working file: prnenv.c
head: 1.3
```
