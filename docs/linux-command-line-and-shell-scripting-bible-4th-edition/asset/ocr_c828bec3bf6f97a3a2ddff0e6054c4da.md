Within the working directory, initialize the `.git/` directory. This task employs the `git init` command:

```
$ git init
Initialized empty Git repository in
/home/christine/MwGuard/.git/
$ ls -ld .git
drwxrwxr-x 7 christine christine 4096 Aug 24 14:49 .git
$
```

The `git init` command creates the `.git/` subdirectory. Because the directory name is preceded with a dot (.), it is hidden from regular `ls` commands. Use the `ls -la` command or add the directory name as an argument to the `ls -ld` command, as we did earlier, in order to view its metadata.

> **NOTE**
> **You can have multiple project directories at the same time. To accomplish this, create a separate working directory for each project.**

If this is the first time you have built a `.git/` subdirectory on your system, add a name and email address to the global Git repository’s configuration file. This identification data helps in tracking file changes, especially if you have several people involved in the project. To perform this task, use the `git config` command:

```
$ git config --global user.name "Christine Bresnahan"
$
$ git config --global user.email "cbresn1723@gmail.com"
$
$ git config --get user.name
Christine Bresnahan
$
$ git config --get user.email
cbresn1723@gmail.com
$
```

By including `--global` on the `git config` command, the `user.name` and