# SEARCH PATTERNS (REGULAR EXPRESSIONS) 281

slightly different formats) some lines of context around the changes, the changes can also be implemented manually if needed. Generally, however, changes are implemented using the `patch` program.

Since the changes between individual versions of the LINUX kernel are published as patches, we are going to use these patches as an example. First of all, we look at the beginning of a file patch (Listing 10.23) by means of the head program (see also Section 10.7.4). The patch contains the names of the modified files in the `linux` path.

If the patch is carried out inside the directory `/usr/src/`, the complete path must be preserved using the option `-p0`. Normally, this option could be omitted, but if new files are created, they will be created in the wrong directory.

If the patch is carried out inside the directory `/usr/src/linux`, the first directory name can be removed using the option `-p1`. Setting the option `-s` screens messages to be displayed only in the event of an error.

```
(Linux):/usr/src# zcat 1.2-patches/patch-1.2.13.gz | head
diff -u -r -N v1.12/linux/Makefile linux/Makefile
--- v1.12/linux/Makefile      Tue Jul 25 12:39:54 1995
++ linux/Makefile             Wed Jul 26 09:43:44 1995
@@ -1,6 +1,6 @@
 VERSION = 1
 PATCHLEVEL = 2
 -SUBLEVEL = 12
 +SUBLEVEL = 13
```

**Listing 10.23** The beginning of a kernel patch.

# 10.3 Search patterns (regular expressions)

A *search pattern* (also known as a 'regular expression' or RE) is an expression, or a template, that is compared with a character string. Often, search patterns are employed to determine whether a given character string matches the pattern (for example, by the `grep` command), or to substitute one character string with another (for example, by the `sed` command).

Regular expressions are used by many UNIX programs, such as `awk`, `sed`, `grep`, and `perl`. Each of these programs uses some of the expressions described in this section, with a slightly different meaning. In your own programs, you can use the corresponding functions (`regcomp()`),