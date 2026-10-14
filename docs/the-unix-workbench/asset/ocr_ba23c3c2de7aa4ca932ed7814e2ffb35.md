```
## [master 53a1983] added two files
## 3 files changed, 1 insertion(+)
## create mode 100644 fil2.txt
## create mode 100644 file1.txt
```

Darn it, now looking at this commit summary I realize that I have a typo in one of the names of my files! Thankfully we can undo the most recent commit with the command git reset --soft HEAD~:

```
git reset --soft HEAD~
git status
```

```
## On branch master
## Changes to be committed:
##   (use "git reset HEAD <file>..." to unstage)
##
##       new file:   fil2.txt
##       new file:   file1.txt
##       modified:   readme.txt
##
```

This repo is now in that exact same state it was right before we made the commit. Now we can rename fil2.txt to file2.txt, then let’s look at the status of the repository again.

```
mv fil2.txt file2.txt
git status
```