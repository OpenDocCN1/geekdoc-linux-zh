
# CONFIGURATION

### rebase.stat

Whether to show a diffstat of what changed upstream since the last rebase. False by default.

### rebase.autoSquash

If set to true enable `--autosquash` option by default.

### rebase.autoStash

If set to true enable `--autostash` option by default.

# OPTIONS

### `--onto <newbase>`

Starting point at which to create the new commits. If the `--onto` option is not specified, the starting point is `<upstream>`. May be any valid commit, and not just an existing branch name.

As a special case, you may use “A..B” as a shortcut for the merge base of A and B if there is exactly one merge base. You can leave out at most one of A and B, in which case it defaults to HEAD.

### `<upstream>`

Upstream branch to compare against. May be any valid commit, not just an existing branch name. Defaults to the configured upstream for the current branch.

### `<branch>`

Working branch; defaults to HEAD.

### `--continue`

Restart the rebasing process after having resolved a merge conflict.

### `--abort`

Abort the rebase operation and reset HEAD to the original branch. If `<branch>` was provided when the rebase operation was started, then HEAD will be reset to `<branch>`. Otherwise HEAD will be reset to where it was when the rebase operation was started.

### `--keep-empty`

Keep the commits that do not change anything from its parents in the result.

### `--skip`

Restart the rebasing process by skipping the current patch.

### `--edit-todo`

Edit the todo list during an interactive rebase.

### `-m`, `--merge`

Use merging strategies to rebase. When the recursive (default) merge strategy is used, this allows rebase to be aware of renames on the upstream side.

Note that a rebase merge works by replaying each commit from the working branch on top of the `<upstream>` branch. Because of this, when a merge conflict happens, the side reported as *ours* is the so-far rebased series, starting with `<upstream>`, and *theirs* is the working branch. In other words, the sides are swapped.

### `-s <strategy>`, `--strategy=<strategy>`

Use the given merge strategy. If there is no `-s` option, `git merge-recursive` is used instead. This implies `--merge`.

Because `git rebase` replays each commit from the working branch on top of the `<upstream>` branch using the given strategy, using the `ours` strategy simply discards all patches from the `<branch>`, which makes little sense.

### `-X <strategy-option>`, `--strategy-option=<strategy-option>`

Pass the `<strategy-option>` through to the merge strategy. This implies `--merge` and, if no strategy has been specified, `-s recursive`. Note the reversal of `ours` and `theirs` as noted above for the `-m` option.

### `-S[<keyid>]`, `--gpg-sign[=<keyid>]`

GPG-sign commits.

### `-q`, `--quiet`

Be quiet. Implies `--no-stat`.

### `-v`, `--verbose`

Be verbose. Implies `--stat`.

### `--stat`

Show a diffstat of what changed upstream since the last rebase. The diffstat is also controlled by the configuration option `rebase.stat`.

### `-n`, `--no-stat`

Do not show a diffstat as part of the rebase process.

### `--no-verify`

This option bypasses the pre-rebase hook. See also `git-hook(5)`.

### `--verify`

Allows the pre-rebase hook to run, which is the default. This option can be used to override `--no-verify`. See also `git-hook(5)`.

### `-C<n>`

Ensure at least `<n>` lines of surrounding context match before and after each change. When fewer lines of surrounding context exist, they all must match. By default, no context is ever ignored.

### `-f`, `--force-rebase`

Force a rebase even if the current branch is up-to-date and the command without `--force` would return without doing anything.

You may find this (or `--no-ff` with an interactive rebase) helpful after reverting a topic branch merge, as this option recreates the topic branch with fresh commits so it can be remerged successfully without needing to "revert the reversion" (see the revert-a-faulty-merge How-To[10] for details).

### `--fork-point`, `--no-fork-point`

Use `git rev-list` to find a better common ancestor between `<upstream>` and `<branch>` when calculating which commits have been introduced by `<branch>`.

When `--fork-point` is active, `fork_point` will be used instead of `<upstream>` to calculate the set of commits to rebase, where `fork_point` is the result of `git merge-base --fork-point <upstream> <branch>` command (see `git-merge-base(1)`). If `fork_point` ends up being empty, the `<upstream>` will be used as a fallback.

If either `<upstream>` or `--root` is given on the command line, then the default is `--no-fork-point`, otherwise the default is `--fork-point`.

### `--ignore-whitespace`, `--whitespace=<option>`

These flags are passed to the `git apply` program (see `git-apply(1)`) that applies the patch. Incompatible with the `--interactive` option.

### `--committer-date-is-author-date`, `--ignore-date`

These flags are passed to `git am` to easily change the dates of the rebased commits (see `git-am(1)`). Incompatible with the `--interactive` option.

### `-i`, `--interactive`

Make a list of the commits which are about to be rebased. Let the user edit that list before rebasing. This mode can also be used to split commits (see SPLITTING COMMITS below).

### `-p`, `--preserve-merges`

Recreate merge commits instead of flattening the history by replaying commits a merge commit introduces. Merge conflict resolutions or manual amendments to merge commits are not preserved.

This uses the `--interactive` machinery internally, but combining it with the `--interactive` option explicitly is generally not a good idea unless you know what you are doing (see BUGS below).

### `-x <cmd>`, `--exec <cmd>`

Append “exec <cmd>” after each line creating a commit in the final history. `<cmd>` will be interpreted as one or more shell commands.

This option can only be used with the `--interactive` option (see INTERACTIVE MODE below).

You may execute several commands by either using one instance of `--exec` with several commands:

```
git rebase -i --exec "cmd1 && cmd2 && ..."
```

or by giving more than one `--exec`:

```
git rebase -i --exec "cmd1" --exec "cmd2"
```
