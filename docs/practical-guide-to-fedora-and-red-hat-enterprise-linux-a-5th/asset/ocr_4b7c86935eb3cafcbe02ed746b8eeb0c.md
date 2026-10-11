To practice generating filenames, you can use `echo` and `ls`. The `echo` utility displays the arguments that the shell passes to it:

```
$ echo may?report
may.report may4report may_report mayreport
```

The shell first expands the ambiguous `file` reference into a list of all `files` in the working directory that match the string `may?report` and then passes this list to `echo`, as though you had entered the list of filenames as arguments to `echo`. Next `echo` displays the list of filenames.

A question mark does not match a leading period (one that indicates a hidden filename; see page 192). When you want to match filenames that begin with a period, you must explicitly include the period in the ambiguous `file` reference.

# THE * SPECIAL CHARACTER

The asterisk (* ) performs a function similar to that of the question mark but matches any number of characters, *including zero characters*, in a filename. The following example shows all of the `files` in the working directory and then shows three commands that display all the filenames that begin with the string `memo`, end with the string `mo`, and contain the string `a`:

```
$ ls
amemo memomemoa memoalx.0620 memosally user.memo
mem memo.0612 memoalx.keep sallymemo
memoalx memoa memorandum typescript
$ echo *memo*
amemo memo.0612 memoa memoalx.0620 memoalx.keep memorandum memosally
$ echo *mo
amemo memo sallymemo user.memo
$ echo *alx*
memoalx memoalx.0620 memoalx.keep
```

The ambiguous file reference `*emo*` does not match **amemo**, **mem**, **sallymemo**, or **user.mem**. Like the question mark, an asterisk does *not* match a leading period in a filename.

The -a option causes `ls` to display hidden filenames. The command `echo *` does not display `.` (the working directory), `..` (the parent of the working directory), `.aaa`, or `.profile`. In contrast, the command `echo . *` displays only those four names:

```
$ ls
aaa memosally sally.0612 thurs
memo.0612 report saturday
$ ls -a
.
.. .aaa aaa memosally sally.0612 thurs
.. ..profile memo.0612 report saturday
$ echo * 
. .aa. .profile
$ echo . * 
. .aa .aaa .profile
```