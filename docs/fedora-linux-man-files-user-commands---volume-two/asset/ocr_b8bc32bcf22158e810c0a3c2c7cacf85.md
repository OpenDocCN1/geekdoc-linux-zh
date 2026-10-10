```
$ git checkout -b foo (1) $ git branch foo (2) $ git tag foo (3)
```

**1.** creates a new branch \textit{foo}, which refers to commit \textit{f}, and then updates HEAD to refer to branch \textit{foo}. In other words, we'll no longer be in detached HEAD state after this command. **2.** similarly creates a new branch \textit{foo}, which refers to commit \textit{f}, but leaves HEAD detached. **3.** creates a new tag \textit{foo}, which refers to commit \textit{f}, leaving HEAD detached.

If we have moved away from commit \textit{f}, then we must first recover its object name (typically by using git reflog), and then we can create a reference to it. For example, to see the last two commits to which HEAD referred, we can use either of these commands:

```
$ git reflog -2 HEAD # or $ git log -g -2 HEAD
```