something while they did nothing)

The *git write-tree* command refuses to write a nonsensical tree, and it will complain about unmerged entries if it sees a single entry that is not stage 0.

OK, this all sounds like a collection of totally nonsensical rules, but it’s actually exactly what you want in order to do a fast merge. The different stages represent the “result tree” (stage 0, aka “merged”), the original tree (stage 1, aka “orig”), and the two trees you are trying to merge (stage 2 and 3 respectively).

The order of stages 1, 2 and 3 (hence the order of three <tree-ish> command-line arguments) are significant when you start a 3-way merge with an index file that is already populated. Here is an outline of how the algorithm works:

+   - if a file exists in identical format in all three trees, it will automatically collapse to “merged” state by *git read-tree*.
+   - a file that has *any* difference what-so-ever in the three trees will stay as separate entries in the index. It’s up to “porcelain policy” to determine how to remove the non-0 stages, and insert a merged version.
+   - the index file saves and restores with all this information, so you can merge things incrementally, but as long as it has entries in stages 1/2/3 (i.e., “unmerged entries”) you can’t write the result. So now the merge algorithm ends up being really simple:
+       - you walk the index in order, and ignore all entries of stage 0, since they’ve already been done.
+       - if you find a “stage1”, but no matching “stage2” or “stage3”, you know it’s been removed from both trees (it only existed in the original tree), and you remove that entry.
+       - if you find a matching “stage2” and “stage3” tree, you remove one of them, and turn the other into a “(stage0)” entry. Remove any matching “stage1” entry if it exists too... all the normal trivial rules ..

You would normally use *git merge-index* with supplied *git merge-one-file* to do this last step. The script updates the files in the working tree as it merges each path and at the end of a successful merge.

When you start a 3-way merge with an index file that is already populated, it is assumed that it represents the state of the files in your work tree, and you can even have files with changes unrecorded in the index file. It is further assumed that this state is “derived” from the stage 2 tree. The 3-way merge refuses to run if it finds an entry in the original index file that does not match stage 2.

This is done to prevent you from losing your work-in-progress changes, and mixing your random changes in an unrelated merge commit. To illustrate, suppose you start from what has been committed last to your repository:

```
$ JG=‘git rev-parse --verify "HEAD^0"` $ git checkout-index -f -u -a $JG
```