entries in a directory tree. You give it pointer to a function which it calls for each object it encounters, but it’s more interesting for us to implement our own tree-walking function, using what we’ve learned in this chapter.

The first thing to clear up is whether the directory structure is really a tree, because our recursive algorithm depends on that. If there are any loops our program might get stuck, and if the same directory is linked to twice (by entries other than . and ..), we might visit the same directory (and its subtree) more than once. There are two kinds of problems to think about:

+   1. It’s pretty common for symbolic links to link to a directory, and that creates at least two links, since every directory is also hard linked to. There’s no protection against symbolic links creating a loop, either.

+   2. On some systems the superuser can create a second hard link to a directory, with the link system call. This is almost never done, but it’s a possibility our program might encounter.

Problem 1 can easily be dealt with by simply not following any symbolic links. We’ll ignore Problem 2 for now, although Exercise 3.5 at the end of this chapter deals with it. So, for our purposes, the tree formed by hard links is indeed a tree.

We want our program, au1s (an extension of the one presented in Section 3.5.3) to act somewhat like 1s, in that a -R argument makes it recurse, and a -d argument tells it to just list the information for a directory, rather than for that directory’s contents. Without either of these arguments it behaves like the earlier au1s.

With the -R argument, au1s (like 1s) first lists the path to a directory and all of the entries at that level, including directories, and then for each directory does the same thing, recursively, as in this example:

```
$ au1s -R /aup/common

/aup/common:
-rwxr-xr-x    1 root     root        1145 Oct  2 10:21 makefile
-rwxr-xr-x    1 root     root         171 Aug 23 10:41 logf.h
-rwxr-xr-x    1 root     root        1076 Aug 26 15:24 logf.c
drwxr-xr-x    1 root     root         4096 Oct  2 12:20 cf
-rwxr-xr-x    1 root     root         245 Aug 26 15:29 notes.txt

/aup/common/cf:
-rwxr-xr-x    1 root     root        1348 Oct  3 13:52 cf-ec.c-ec_push.htm
-rwxr-xr-x    1 root     root         576 Oct  3 13:52 cf-ec.c-ec_print.htm
```