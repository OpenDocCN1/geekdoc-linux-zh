
## OPTIONS

- `-n, --dry-run`
  Do not remove anything; just report what it would remove.
- `-v, --verbose`
  Report all removed objects.
- `--`
  Do not interpret any more arguments as options.
- `--expire <time>`
  Only expire loose objects older than `<time>`.
- `<head>…`
  In addition to objects reachable from any of our references, keep objects reachable from listed `<head>`s.

## EXAMPLE

To prune objects not used by your repository or another that borrows from your repository via its `.git/objects/info/alternates`:

```bash
$ git prune $(cd ../another && git rev-parse --all)
```

## NOTES

In most cases, users will not need to call *git prune* directly, but should instead call *git gc*, which handles pruning along with many other housekeeping tasks.

For a description of which objects are considered for pruning, see *git fsck*'s `--unreachable` option.

## SEE ALSO

`git-gc(1)`, `git-repack(1)`, `git-prune(1)`

# GIT-PULL

## NAME

git-pull - Fetch from and integrate with another repository or a local branch

## SYNOPSIS

*git pull* [options] [<repository> [<refspec>...]]

## DESCRIPTION

Incorporates changes from a remote repository into the current branch. In its default mode, *git pull* is shorthand for *git fetch* followed by *git merge FETCH_HEAD*.
More precisely, *git pull* runs *git fetch* with the given parameters and calls *git merge* to merge the retrieved branch heads into the current branch. With `--rebase`, it runs *git rebase* instead of *git merge*.

<repository> should be the name of a remote repository as passed to `git-fetch(1)`. <refspec> can name an arbitrary remote ref (for example, the name of a tag) or even a collection of refs with corresponding remote-tracking branches (e.g., `refs/heads/*:refs/remotes/origin/*`), but usually it is the name of a branch in the remote repository.

Default values for <repository> and <branch> are read from the “remote” and “merge” configuration for the current branch as set by `git-branch(1) --track`.

Assume the following history exists and the current branch is “master”:

```text
A---B---C master on origin
/
D---E---F---G master ^ origin/master in your repository
```

Then “*git pull*” will fetch and replay the changes from the remote master branch since it diverged from the local master (i.e., E) until its current commit (C) on top of master and record the result in a new commit along with the names of the two parent commits and a log message from the user describing the changes.

```text
A---B---C origin/master
      \
D---E---F---G---H master
```

See `git-merge(1)` for details, including how conflicts are presented and handled.

In Git 1.7.0 or later, to cancel a conflicting merge, use *git reset* `--merge`. **Warning**: In older versions of Git, running *git pull* with uncommitted changes is discouraged: while possible, it leaves you in a state that may be hard to back out of in the case of a conflict. If any of the remote changes overlap with local uncommitted changes, the merge will be automatically cancelled and the work tree untouched. It is generally best to get any local changes in working order before pulling or stash them away with `git-stash(1)`.

## OPTIONS

- `-q`, `--quiet`
  This is passed to both underlying git-fetch to squelch reporting of during transfer, and underlying git-merge to squelch output during merging.
- `-v`, `--verbose`
  Pass `--verbose` to git-fetch and git-merge.
- `--[no-]recurse-submodules[={=yes|on-demand|no}]`
  This option controls if new commits of all populated submodules should be fetched too (see `git-fetch(1)` and `git-submodule(5)`). That might be necessary to get the data needed for merging submodule commits, a feature Git learned in 1.7.3. Notice that the result of a merge will not be checked out in the submodule, "git submodule update" has to be called afterwards to bring the work tree up to date with the merge result.

### Options related to merging

- `--commit`, `--no-commit`
  Perform the merge and commit the result. This option can be used to override `--no-commit`.
  With `--no-commit` perform the merge but pretend the merge failed and do not autocommit, to give the user a chance to inspect and further tweak the merge result before committing.
- `--edit`, `-e`, `--no-edit`
  Invoke an editor before committing successful mechanical merge to further edit the auto-generated merge message, so that the user can explain and justify the merge. The `--no-edit` option can be used to accept the auto-generated message (this is generally discouraged).
  Older scripts may depend on the historical behaviour of not allowing the user to edit the merge log message. They will see an editor opened when they run git merge. To make it easier to adjust such scripts to the updated behaviour, the environment variable `GIT_MERGE_AUTOEDIT` can be set to no at the beginning of them.
- `--ff`
  When the merge resolves as a fast-forward, only update the branch pointer, without creating a merge commit. This is the default behavior.
- `--no-ff`
  Create a merge commit even when the merge resolves as a fast-forward. This is the default behaviour when merging an annotated (and possibly signed) tag.
- `--ff-only`
  Refuse to merge and exit with a non-zero status unless the current HEAD is already up-to-date or the merge can be resolved as a fast-forward.
- `--log[=<n>]`, `--no-log`
  In addition to branch names, populate the log message with one-line descriptions from at most <n> actual commits that are being merged. See also `git-log(1)`.
  With `--no-log` do not list one-line descriptions from the actual commits being merged.
- `--stat`, `-n`, `--no-stat`
  Show a diffstat at the end of the merge. The diffstat is also controlled by the configuration option `merge.stat`.
  With `-n` or `--no-stat` do not show a diffstat at the end of the merge.
- `--squash`, `--no-squash`
  Produce the working tree and index state as if a real merge happened (except for the merge information), but do not actually make a commit, move the HEAD, or record `$GIT_DIR/MERGE_HEAD` (to cause the next git commit command to create a merge commit). This allows you to create a single commit on top of the current branch whose effect is the same as merging another branch (or more in case of an octopus).
  With `--no-squash` perform the merge and commit the result. This option can be used to override `--squash`.
- `-s <strategy>`, `--strategy=<strategy>`
  Use the given merge strategy; can be supplied more than once to specify them in the order they should be tried. If there is no `-s` option, a built-in list of strategies is used instead (`git merge-recursive` when merging a single head, `git merge-octopus` otherwise).
- `-X <option>`, `--strategy-option=<option>`
  Pass merge strategy specific option through to the merge strategy.
- `--verify-signatures`, `--no-verify-signatures`
  Verify that the commits being merged have good and trusted GPG signatures and abort the merge in case they do not.
- `--summary`, `--no-summary`
  Synonyms to `--stat` and `--no-stat`; these are deprecated and will be removed in the future.
- `-r`, `--rebase[=false|true|preserve]`
  When true, rebase the current branch on top of the upstream branch after fetching. If there is a remote-tracking branch corresponding to the upstream branch and the upstream branch was rebased since last fetched, the rebase uses that information to avoid rebasing non-local changes.
  When set to **preserve**, rebase with the `--preserve-merges` option passed to `git rebase` so that locally created merge commits will not be flattened.
  When false, merge the current branch into the upstream branch.
  See `pull.rebase`, `branch.<name>.rebase` and `branch.autoSetupRebase` in `git-config(1)` if you want to make `git pull` always use `--rebase` instead of merging.
  **Note** This is a potentially *dangerous* mode of operation. It rewrites history, which does not bode well when you published that history already. Do **not** use this option unless you have read `git-rebase(1)` carefully.
- `--no-rebase`
  Override earlier `--rebase`.

### Options related to fetching

- `--all`
  Fetch all remotes.
- `-a`, `--append`
  Append ref names and object names of fetched refs to the existing contents of `.git/FETCH_HEAD`. Without this option old data in `.git/FETCH_HEAD` will be overwritten.
- `--depth=<depth>`
  Deepen or shorten the history of a *shallow* repository created by `git clone` with `--depth=<depth>` option (see `git-clone(1)`) to the specified number of commits from the tip of each remote branch history. Tags for the deepened commits are not fetched.
- `--unshallow`
  If the source repository is complete, convert a shallow repository to a complete one, removing all the limitations imposed by shallow repositories.
  If the source repository is shallow, fetch as much as possible so that the current repository has the same history as the source repository.
- `--update-shallow`
  By default when fetching from a shallow repository, `git fetch` refuses refs that require updating `.git/shallow`. This option updates `.git/shallow` and accept such refs.
- `-f`, `--force`
  When `git fetch` is used with `<rbranch>:<lbranch>` refspec, it refuses to update the local branch `<lbranch>` unless the remote branch `<rbranch>` it fetches is a descendant
