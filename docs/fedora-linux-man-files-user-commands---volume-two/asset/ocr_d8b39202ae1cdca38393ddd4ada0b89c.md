# ## **EXAMPLES**

```
git cherry-pick master
```

Apply the change introduced by the commit at the tip of the master branch and create a new commit with this change.

```
git cherry-pick ..master, git cherry-pick ^HEAD master
```

Apply the changes introduced by all commits that are ancestors of master but not of HEAD to produce new commits.

```
git cherry-pick maint next ^master, git cherry-pick maint master..next
```

Apply the changes introduced by all commits that are ancestors of maint or next, but not master or any of its ancestors. Note that the latter does not mean maint and everything between master and next; specifically, maint will not be used if it is included in master.

```
git cherry-pick master~4 master~2
```

Apply the changes introduced by the fifth and third last commits pointed to by master and create 2 new commits with these changes.

```
git cherry-pick -n master~1 next
```

Apply to the working tree and the index the changes introduced by the second last commit pointed to by master and by the last commit pointed to by next, but do not create any commit with these changes.

```
git cherry-pick —ff ..next
```

If history is linear and HEAD is an ancestor of next, update the working tree and advance the HEAD pointer to match next. Otherwise, apply the changes introduced by those commits that are in next but not HEAD to the current branch, creating a new commit for each new change.

```
git rev-list —reverse master — README | git cherry-pick -n —stdin
```

Apply the changes introduced by all commits on the master branch that touched README to the working tree and index, so the result can be inspected and made into a single new commit if suitable.

The following sequence attempts to backport a patch, bails out because the code the patch applies to has changed too much, and then tries again, this time exercising more care about matching up context lines.

```
$ git cherry-pick topic^ (1) $ git diff (2) $ git reset --merge ORIG_HEAD (3) $ git cherry-pick -Xpatience topic^ (4)
```

+   1. apply the change that would be shown by `git show topic^`. In this example, the patch does not apply cleanly, so information about the conflict is written to the index and working tree and no new commit results.
+   2. summarize changes to be reconciled
+   3. cancel