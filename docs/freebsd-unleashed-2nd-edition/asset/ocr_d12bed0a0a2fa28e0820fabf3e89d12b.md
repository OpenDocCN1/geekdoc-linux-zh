# ## Exit Status

Most programs in FreeBSD return an exit status when they terminate. The exit status is usually 0 if successful, and some number other than 0 if something went wrong. Some programs will return a different exit status, depending on the problem. Often, this information can be found in the program's man page.

The exit status of the last program that ran is stored in the magic variable $?. Here are a couple of examples:

```
```
  bash$ ls > /dev/null
  bash$ echo $?
  0
  bash$

  bash$ ls -2 /dev/null
  ls: illegal option - - 2
  usage: ls [-ABCDFGHLOPRSTWabcfgiklnopqrstux] [file ...]
  bash$ echo $?
  1
  bash$
```
```

The first example will set the magic variable $? to 0, as shown (the output of the ls command was redirected to /dev/null for brevity in the example). The second example, however, supplies an illegal option to ls. The command fails with an error message, and $? is set to 1.

You can use this exit status to make automatic decisions in your shell programs. The previous logical AND/OR example already introduced this to an extent. It showed how the success or failure of one command can determine whether the next one is executed. The logical AND/OR statement used in the previous section could also have been written as an if statement, like this:

```
```
 if tar cvfz backup.tar.gz documents/2000/*
 then
 rm -r documents/2000
 else
 echo "Archive operation failed"
 fi
```
```

This example combines the two examples from the previous section. The if statement reads the exit status of the tar command. If the exit status is 0, the then statements are performed, and the directory that was archived is removed. If the exit status is some