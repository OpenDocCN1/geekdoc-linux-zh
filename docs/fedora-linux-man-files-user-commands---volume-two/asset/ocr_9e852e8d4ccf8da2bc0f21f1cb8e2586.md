—conflict=<style>

The same as —merge option above, but changes the way the conflicting hunks are presented, overriding the merge.conflictStyle configuration variable. Possible values are “merge” (default) and “diff3” (in addition to what is shown by “merge” style, shows the original contents).

-p, —patch

Interactively select hunks in the difference between the <tree-ish> (or the index, if unspecified) and the working tree. The chosen hunks are then applied in reverse to the working tree (and if a <tree-ish> was specified, the index).

This means that you can use git checkout -p to selectively discard edits from your current working tree. See the “Interactive Mode” section of (1) to learn how to operate the —patch mode.

—ignore-other-worktrees

git checkout refuses when the wanted ref is already checked out by another worktree. This option makes it check the ref out anyway. In other words, the ref can be held by more than one worktree.

<branch>

Branch to checkout; if it refers to a branch (i.e., a name that, when prepended with “refs/heads/”, is a valid ref), then that branch is checked out. Otherwise, if it refers to a valid commit, your HEAD becomes “detached” and you are no longer on any branch (see below for details).

As a special case, the “@{-N}” syntax for the N-th last branch/commit checks out branches (instead of detaching). You may also specify - which is synonymous with “@{-1}”.

As a further special case, you may use “A…B” as a shortcut for the merge base of A and B if there is exactly one merge base. You can leave out at most one of A and B, in which case it defaults to HEAD.

<new_branch>

Name for the new branch.

<start_point>

The name of a commit at which to start the new branch; see (1) for details. Defaults to HEAD.

<tree-ish>

Tree to checkout from (when paths are given). If not specified, the index will be used.