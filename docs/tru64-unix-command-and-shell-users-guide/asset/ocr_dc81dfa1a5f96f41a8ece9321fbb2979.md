If you want to specify a default editor for the -e flag, define the FCEDIT variable in your .profile script. For example, if you want to make emacs your default editor, enter the following variable definition:

```
FCEDIT=emacs
```

```
fc -e - [old=new] [string]
```

This command lets you immediately replace an old string with a new string within any previous command line.

+   - The -e - entry specifies that you want to make a replacement.
+   - The old=new entry specifies that you want to replace the old string with the new string.
+   - The string entry specifies that the Korn or POSIX shell should make the edit to the most recent command line in the buffer containing the string.

The following section contains some examples of fc use.

The Korn or POSIX shell also lets you edit individual command lines at the shell prompt by using a command set similar to the vi or the emacs editors. For more information on this feature, see the ksh(1) or sh(1p) reference pages.

# 8.4.4.1 Examples of Command Line Editing

To display command lines 15 to 18, enter the following command:

```
$ fc -l 15 18
15 ls -la
16 pwd
17 cd /u/ben/reports
18 more sales
$
```

You also may list the same command lines by specifying command strings instead of line numbers, as in the following example:

```
$ fc -l ls more
15 ls -la
16 pwd
17 cd /u/ben/reports
18 more sales
$
```

To display and edit command lines 15 to 18 with the vi editor, enter the following command:

```
$ fc -e vi 15 18
ls -la
pwd
```