# > PRE-MERGE CHECKS

Before applying outside changes, you should get your own work in good shape and committed locally, so it will not be clobbered if there are conflicts. See also (1). *git pull* and *git merge* will stop without doing anything when local uncommitted changes overlap with files that *git pull*/*git merge* may need to update.

To avoid recording unrelated changes in the merge commit, *git pull* and *git merge* will also abort if there are any changes registered in the index relative to the HEAD commit. (One exception is when the changed index entries are in the state that would result from the merge already.)

If all named commits are already ancestors of HEAD, *git merge* will exit early with the message “Already up-to-date.”