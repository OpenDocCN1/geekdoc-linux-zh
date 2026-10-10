
## EXAMPLES

To update and refresh only the files already checked out:

```bash
$ git checkout-index -n -f -a && git update-index --ignore-missing --refresh
```

Using git checkout-index to “export an entire tree”

The prefix ability basically makes it trivial to use git checkout-index as an “export as tree” function. Just read the desired tree into the index, and do:

```bash
$ git checkout-index --prefix=git-export-dir/ -a
```

git checkout-index will “export” the index into the specified directory.

The final “/” is important. The exported name is literally just prefixed with the specified string. Contrast this with the following example.

Export files with a prefix

```bash
$ git checkout-index --prefix=.merged- Makefile
```

This will check out the currently cached copy of Makefile into the file .merged-Makefile.

# GIT-CHECKOUT

## NAME

git-checkout - Switch branches or restore working tree files

## SYNOPSIS

```bash
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach <branch>
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B]--orphan] <new_branch> [<start_point>]
git checkout [-f|--ours|--theirs|-m|--conflict=<style>] [<tree-ish>] [-] <paths>...
git checkout [-p|--patch] [<tree-ish>] [--] [<paths>...]
```

## DESCRIPTION

Updates files in the working tree to match the version in the index or the specified tree. If no paths are given, git checkout will also update HEAD to set the specified branch as the current branch.

### git checkout <branch>

To prepare for working on <branch>, switch to it by updating the index and the files in the working tree, and by pointing HEAD at the branch. Local modifications to the files in the working tree are kept, so that they can be committed to the <branch>.

If <branch> is not found but there does exist a tracking branch in exactly one remote (call it <remote>) with a matching name, treat as equivalent to

```bash
$ git checkout -b <branch> --track <remote>/<branch>
```

You could omit <branch>, in which case the command degenerates to “check out the current branch”, which is a glorified no-op with a rather expensive side-effects to show only the tracking information, if exists, for the current branch.

### git checkout -b|-B <new_branch> [<start point>]

Specifying -b causes a new branch to be created as if (1) were called and then checked out. In this case you can use the --track or --no-track options, which will be passed to git branch. As a convenience, --track without -b implies branch creation; see the description of --track below.

If -B is given, <new_branch> is created if it doesn’t exist; otherwise, it is reset. This is the transactional equivalent of

```bash
$ git branch -f <branch> [<start point>]
$ git checkout <branch>
```

that is to say, the branch is not reset/created unless “git checkout” is successful.

### git checkout --detach [<branch>], git checkout [--detach] <commit>

Prepare to work on top of <commit>, by detaching HEAD at it (see “DETACHED HEAD” section), and updating the index and the files in the working tree. Local modifications to the files in the working tree are kept, so that the resulting working tree will be the state recorded in the commit plus the local modifications.

When the <commit> argument is a branch name, the --detach option can be used to detach HEAD at the tip of the branch (git checkout <branch> would check out that branch without detaching HEAD).

Omitting <branch> detaches HEAD at the tip of the current branch.

### git checkout [-p|--patch] [<tree-ish>] [--] <pathspec> ...

When <paths> or --patch are given, git checkout does not switch branches. It updates the named paths in the working tree from the index file or from a named <tree-ish> (most often a commit). In this case, the -b and --track options are meaningless and giving either of them results in an error. The <tree-ish> argument can be used to specify a specific tree-ish (i.e. commit, tag or tree) to update the index for the given paths before updating the working tree.

git checkout with <paths> or --patch is used to restore modified or deleted paths to their original contents from the index or replace paths with the contents from a named <tree-ish> (most often a commit-ish).

The index may contain unmerged entries because of a previous failed merge. By default, if you try to check out such an entry from the index, the checkout operation will fail and nothing will be checked out. Using -f will ignore these unmerged entries. The contents from a specific side of the merge can be checked out of the index by using --ours or --theirs. With -m, changes made to the working tree file can be discarded to re-create the original conflicted merge result.

## OPTIONS

- -q, --quiet
  Quiet, suppress feedback messages.

- -f, --force
  When switching branches, proceed even if the index or the working tree differs from HEAD. This is used to throw away local changes.
  When checking out paths from the index, do not fail upon unmerged entries; instead, unmerged entries are ignored.

- --ours, --theirs
  When checking out paths from the index, check out stage #2 (*ours*) or #3 (*theirs*) for unmerged paths.

- -b <new_branch>
  Create a new branch named <new_branch> and start it at <start_point>; see (1) for details.

- -B <new_branch>
  Creates the branch <new_branch> and start it at <start_point>; if it already exists, then reset it to <start_point>. This is equivalent to running “git branch” with “-f”; see (1) for details.

- -t, --track
  When creating a new branch, set up “upstream” configuration. See “--track” in (1) for details.
  If no -b option is given, the name of the new branch will be derived from the remote-tracking branch, by looking at the local part of the refspec configured for the corresponding remote, and then stripping the initial part up to the “*”. This would tell us to use “hack” as the local branch when branching off of “origin/hack” (or “remotes/origin/hack”, or even “refs/remotes/origin/hack”). If the given name has no slash, or the above guessing results in an empty name, the guessing is aborted. You can explicitly give a name with -b in such a case.

- --no-track
  Do not set up “upstream” configuration, even if the branch.autoSetupMerge configuration variable is true.

- -1
  Create the new branch’s reflog; see (1) for details.

- --detach
  Rather than checking out a branch to work on it, check out a commit for inspection and discardable experiments. This is the default behavior of "git checkout <commit>" when <commit> is not a branch name. See the "DETACHED HEAD" section below for details.

- --orphan <new_branch>
  Create a new orphan branch, named <new_branch>, started from <start_point> and switch to it. The first commit made on this new branch will have no parents and it will be the root of a new history totally disconnected from all the other branches and commits.
  The index and the working tree are adjusted as if you had previously run "git checkout <start_point>". This allows you to start a new history that records a set of paths similar to <start_point> by easily running "git commit -a" to make the root commit.
  This can be useful when you want to publish the tree from a commit without exposing its full history. You might want to do this to publish an open source branch of a project whose current tree is "clean", but whose full history contains proprietary or otherwise encumbered bits of code.
  If you want to start a disconnected history that records a set of paths that is totally different from the one of <start_point>, then you should clear the index and the working tree right after creating the orphan branch by running "git rm -rf ." from the top level of the working tree. Afterwards you will be ready to prepare your new files, repopulating the working tree, by copying them from elsewhere, extracting a tarball, etc.

- --ignore-skip-worktree-bits
  In sparse checkout mode, git checkout -- <paths> would update only entries matched by <paths> and sparse patterns in $GIT_DIR/info/sparse-checkout. This option ignores the sparse patterns and adds back any files in <paths>.

- -m, --merge
  When switching branches, if you have local modifications to one or more files that are different between the current branch and the branch to which you are switching, the command refuses to switch branches in order to preserve your modifications in context. However, with this option, a three-way merge between the current branch, your working tree contents, and the new branch is done, and you will be on the new branch.
  When a merge conflict happens, the index entries for conflicting paths are left unmerged, and you need to resolve the conflicts and mark the resolved paths with git add (or git rm if the merge should result in deletion of the path).
  When checking out paths from the index, this option lets you recreate the conflicted merge in the specified paths.
