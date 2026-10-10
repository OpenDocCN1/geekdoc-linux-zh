
## OPTIONS

- **-n, --dry-run**: Walk through the patches in the series and warn if we cannot find all of the necessary information to commit a patch. At the time of this writing only missing author information is warned about.
- **--author** *Author Name <Author Email>*: The author name and email address to use when no author information can be found in the patch description.
- **--patches** *<dir>*: The directory to find the quilt patches and the quilt series file.
    - The default for the patch directory is `patches` or the value of the `$QUILT_PATCHES` environment variable.

## GIT-READ-TREE

### NAME

git-read-tree – Reads tree information into the index

### SYNOPSIS

```
git read-tree [[-m [--trivial] [--aggressive] | --reset | --prefix=<prefix>] [-u [--exclude-per-directory=<gitignore>] | -i]] [--index-output=<file>] [--no-sparse-checkout] (--empty | <tree-ish1> [<tree-ish2> [<tree-ish3>]])
```

### DESCRIPTION

Reads the tree information given by `<tree-ish>` into the index, but does not actually **update** any of the files it “caches”. (see: (1))

Optionally, it can merge a tree into the index, perform a fast-forward (i.e. 2-way) merge, or a 3-way merge, with the `-m` flag. When used with `-m`, the `-u` flag causes it to also update the files in the work tree with the result of the merge.

Trivial merges are done by `git read-tree` itself. Only conflicting paths will be in unmerged state when `git read-tree` returns.

### OPTIONS

- **-m**: Perform a merge, not just a read. The command will refuse to run if your index file has unmerged entries, indicating that you have not finished previous merge you started.
- **--reset**: Same as `-m`, except that unmerged entries are discarded instead of failing.
- **-u**: After a successful merge, update the files in the work tree with the result of the merge.
- **-i**: Usually a merge requires the index file as well as the files in the working tree to be up to date with the current head commit, in order not to lose local changes. This flag disables the check with the working tree and is meant to be used when creating a merge of trees that are not directly related to the current working tree status into a temporary index file.
- **-n, --dry-run**: Check if the command would error out, without updating the index or the files in the working tree for real.
- **-v**: Show the progress of checking files out.
- **--trivial**: Restrict three-way merge by `git read-tree` to happen only if there is no file-level merging required, instead of resolving merge for trivial cases and leaving conflicting files unresolved in the index.
- **--aggressive**: Usually a three-way merge by `git read-tree` resolves the merge for really trivial cases and leaves other cases unresolved in the index, so that porcelains can implement different merge policies. This flag makes the command resolve a few more cases internally:
    - when one side removes a path and the other side leaves the path unmodified. The resolution is to remove that path.
    - when both sides remove a path. The resolution is to remove that path.
    - when both sides add a path identically. The resolution is to add that path.
- **--prefix=***<prefix>/**: Keep the current index contents, and read the contents of the named tree-ish under the directory at `<prefix>`. The command will refuse to overwrite entries that already existed in the original index file. Note that the `<prefix>/` value must end with a slash.
- **--exclude-per-directory=***<gitignore>*: When running the command with `-u` and `-m` options, the merge result may need to overwrite paths that are not tracked in the current branch. The command usually refuses to proceed with the merge to avoid losing such a path. However this safety valve sometimes gets in the way. For example, it often happens that the other branch added a file that used to be a generated file in your branch, and the safety valve triggers when you try to switch to that branch after you ran `make` but before running `make clean` to remove the generated file. This option tells the command to read per-directory exclude file (usually `.gitignore`) and allows such an untracked but explicitly ignored file to be overwritten.
- **--index-output=***<file>*: Instead of writing the results out to `$GIT_INDEX_FILE`, write the resulting index in the named file. While the command is operating, the original index file is locked with the same mechanism as usual. The file must allow to be (2)ed into from a temporary file that is created next to the usual index file; typically this means it needs to be on the same filesystem as the index file itself, and you need write permission to the directories the index file and index output file are located in.
- **--no-sparse-checkout**: Disable sparse checkout support even if `core.sparseCheckout` is true.
- **--empty**: Instead of reading tree object(s) into the index, just empty it.
- **<tree-ish#>**: The id of the tree object(s) to be read/merged.

### MERGING

If `-m` is specified, `git read-tree` can perform 3 kinds of merge, a single tree merge if only 1 tree is given, a fast-forward merge with 2 trees, or a 3-way merge if 3 trees are provided.

#### Single Tree Merge

If only 1 tree is specified, `git read-tree` operates as if the user did not specify `-m`, except that if the original index has an entry for a given pathname, and the contents of the path match with the tree being read, the stat info from the index is used. (In other words, the index’s stat()s take precedence over the merged tree’s).

That means that if you do a `git read-tree -m` `<newtree>` followed by a `git checkout-index -f -u -a`, the `git checkout-index` only checks out the stuff that really changed.

This is used to avoid unnecessary false hits when `git diff-files` is run after `git read-tree`.

#### Two Tree Merge

Typically, this is invoked as `git read-tree -m` `$H` `$M`, where `$H` is the head commit of the current repository, and `$M` is the head of a foreign tree, which is simply ahead of `$H` (i.e. we are in a fast-forward situation).

When two trees are specified, the user is telling `git read-tree` the following:

1.  The current index and work tree is derived from `$H`, but the user may have local changes in them since `$H`.
2.  The user wants to fast-forward to `$M`.

In this case, the `git read-tree -m` `$H` `$M` command makes sure that no local change is lost as the result of this “merge”. Here are the “carry forward” rules, where “I” denotes the index, “clean” means that index and work tree coincide, and “exists”/“nothing” refer to the presence of a path in the specified commit:

| I | H | Result |
| :--- | :--- | :--- |
| 0 | nothing | nothing |
| 1 | nothing | nothing |
| 2 | nothing | exists use M |
| 3 | nothing | exists |
| | | exists, use M if "initial checkout", H == M keep index otherwise exists, fail H != M |
| clean I==H | I==M | ---------------- |
| 4 | yes | N/A N/A index |
| 5 | no | N/A N/A nothing nothing keep index |
| 6 | yes | N/A yes nothing exists keep index |
| 7 | no | N/A yes nothing exists keep index |
| 8 | yes | N/A no nothing exists fail |
| 9 | no | N/A no nothing exists fail |
| 10 | yes | yes N/A exists nothing remove path from index |
| 11 | no | yes N/A exists nothing fail |
| 12 | yes | no N/A exists nothing fail |
| 13 | no | no N/A exists nothing fail |
| clean (H=M) | | |
| 14 | yes | exists exists keep index |
| 15 | no | exists exists keep index |
| clean I==H | I==M (H!=M) | ------------------ |
| 16 | yes | no no exists exists fail |
| 17 | no | no no exists exists fail |
| 18 | yes | no yes exists exists keep index |
| 19 | no | no yes exists exists keep index |
| 20 | yes | yes no exists exists use M |
| 21 | no | yes no exists exists fail |

In all “keep index” cases, the index entry stays as in the original index file. If the entry is not up to date, `git read-tree` keeps the copy in the work tree intact when operating under the `-u` flag.

When this form of `git read-tree` returns successfully, you can see which of the “local changes” that you made were carried forward by running `git diff-index --cached $M`. Note that this does not necessarily match what `git diff-index --cached $H` would have produced before such a two tree merge. This is because of cases 18 and 19 – if you already had the changes in `$M` (e.g. maybe you picked it up via e-mail in a patch form), `git diff-index --cached $H` would have told you about the change before this merge, but it would not show in `git diff-index --cached $M` output after the two-tree merge.

Case 3 is slightly tricky and needs explanation. The result from this rule logically should be to remove the path if the user staged the removal of the path and then switching to a new branch. That however will prevent the initial checkout from happening, so the rule is modified to use M (new tree) only when the content of the index is empty. Otherwise the removal of the path is kept as long as `$H` and `$M` are the same.

#### 3-Way Merge

Each “index” entry has two bits worth of “stage” state. stage 0 is the normal one, and is the only one you’d see in any kind of normal use.

However, when you do `git read-tree` with three trees, the “stage” starts out at 1. This means that you can do

```
$ git read-tree -m <tree1> <tree2> <tree3>
```

and you will end up with an index with all of the `<tree1>` entries in “stage1”, all of the `<tree2>` entries in “stage2” and all of the `<tree3>` entries in “stage3”. When performing a merge of another branch into the current branch, we use the common ancestor tree as `<tree1>`, the current branch head as `<tree2>`, and the other branch head as `<tree3>`.

Furthermore, `git read-tree` has special-case logic that says: if you see a file that matches in all respects in the following states, it “collapses” back to “stage0”:

- stage 2 and 3 are the same; take one or the other (it makes no difference - the same work has been done on our branch in stage 2 and their branch in stage 3)
- stage 1 and stage 2 are the same and stage 3 is different; take stage 3 (our branch in stage 2 did not do anything since the ancestor in stage 1 while their branch in stage 3 worked on it)
- stage 1 and stage 3 are the same and stage 2 is different take stage 2 (we did
