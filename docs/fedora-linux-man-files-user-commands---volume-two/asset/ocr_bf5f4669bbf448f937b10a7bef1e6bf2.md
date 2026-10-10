Use the given merge strategy. If there is no -s option git merge-recursive is used instead. This implies —merge.

Because git rebase replays each commit from the working branch on top of the <upstream> branch using the given strategy, using the ours strategy simply discards all patches from the <branch>, which makes little sense.

-X <strategy-option>, —strategy-option=<strategy-option>

Pass the <strategy-option> through to the merge strategy. This implies —merge and, if no strategy has been specified, -s recursive. Note the reversal of ours and theirs as noted above for the -m option.

-S[<keyid>], —gpg-sign[=<keyid>]

GPG-sign commits.

-q, —quiet

Be quiet. Implies —no-stat.

-v, —verbose

Be verbose. Implies —stat.

—stat

Show a diffstat of what changed upstream since the last rebase. The diffstat is also controlled by the configuration option rebase.stat.

-n, —no-stat

Do not show a diffstat as part of the rebase process.

—no-verify

This option bypasses the pre-rebase hook. See also (5).

—verify

Allows the pre-rebase hook to run, which is the default. This option can be used to override —no-verify. See also (5).

-C<n>

Ensure at least <n> lines of surrounding context match before and after each change. When fewer lines of surrounding context exist they all must match. By default no context is ever ignored.

-f, —force-rebase

Force a rebase even if the current branch is up-to-date and the command without —force would return without doing anything.

You may find this (or —no-ff with an interactive rebase) helpful after reverting a topic branch merge, as this option recreates the topic branch with fresh commits so it can be remerged successfully without needing to "revert the reversion" (see the