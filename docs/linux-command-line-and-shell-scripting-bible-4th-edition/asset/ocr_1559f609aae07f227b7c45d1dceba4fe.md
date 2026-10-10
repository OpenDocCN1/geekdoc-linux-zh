```
/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
$
```

The directories in the PATH are separated by colons. And this shows that there are nine directories where the shell looks for commands and programs.

If a command's or program's location is not included in the PATH variable, the shell cannot find it without an absolute directory reference. If the shell cannot find the command or program, it produces an error message:

```
$ myprog
myprog: command not found
$
```

The problem is that sometimes applications place their executable programs in directories that aren't in the PATH environment variable. The trick is to ensure your PATH environment variable includes all the directories where your applications reside.

> **NOTE**
> 
> Some script builders use the *env* command as the first line in a Bash shell script (covered in **Chapter 11**, “Basic Script Building”) as in the following: `#!/usr/bin/env bash`. The advantage of this method is that the *env* utility searches for the *bash* shell program within the `$PATH` directories, making the script more portable to other Linux distributions.

You can add new search directories to the existing PATH environment variable without having to rebuild it from scratch. The individual directories listed in the PATH are separated by colons. All you need to do is reference the original PATH value, add a colon (:), and type in the new directory using an absolute directory reference. On a CentOS Linux system, it looks something like this:

```
$ ls /home/christine/Scripts/
myprog
```