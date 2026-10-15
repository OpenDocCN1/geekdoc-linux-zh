5. Compile hello.c, and list the files in the current working directory.

```
% gcc47 hello.c
% ls
a.out  hello.c
%
```

6. Use the git status command to examine the status of the repository at this point. It will show you that you are on the branch named master, you can do your initial commit, the untracked files are a.out and hello.c, and you can stage those files by using git add.

```
% git status
On branch master
Initial commit
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    a.out
    hello.c
nothing added to commit but untracked files present (use "git add" to track)
%
```

7. Stage only the source code file hello.c with the git add command.

```
% git add hello.c
%
```

8. Now do your initial commit.

```
% git commit
%
```

Use the default text editor to put the message Added the Hello Linus program on the first line of the file that appears, and then save and quit that file.

```
/usr/home/bob/short-git/.git/COMMIT_EDITMSG: 13 lines, 285 characters.
[master (root-commit) 0527389] Added the Hello Linus program
 1 file changed, 6 insertions(+)
 create mode 100644 hello.c
```

9. Look at the status of the repository.

```
% git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
    a.out
```