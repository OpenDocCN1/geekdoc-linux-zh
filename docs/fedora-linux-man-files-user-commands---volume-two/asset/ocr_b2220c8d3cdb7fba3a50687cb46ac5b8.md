# OPTIONS

-a, --all

Tell the command to automatically stage files that have been modified and deleted, but new files you have not told Git about are not affected.

-p, --patch

Use the interactive patch selection interface to chose which changes to commit. See (1) for details.

-C <commit>, --reuse-message=<commit>

Take an existing commit object, and reuse the log message and the authorship information (including the timestamp) when creating the commit.

-c <commit>, --reedit-message=<commit>

Like -C, but with -c the editor is invoked, so that the user can further edit the commit message.

--fixup=<commit>

Construct a commit message for use with rebase --autosquash. The commit message will be the subject line from the specified commit with a prefix of “fixup! “. See (1) for details.

--squash=<commit>

Construct a commit message for use with rebase --autosquash. The commit message subject line is taken from the specified commit with a prefix of “squash! “. Can be used with additional commit message options (-m/-c/-C/-F). See (1) for details.

--reset-author

When used with -C/-c/--amend options, or when committing after a a conflicting cherry-pick, declare that the authorship of the resulting commit now belongs to the committer. This also renews the author timestamp.

--short

When doing a dry-run, give the output in the short-format. See (1) for details. Implies --dry-run.

--branch

Show the branch and tracking info even in short-format.

--porcelain

When doing a dry-run, give the output in a porcelain-ready format. See (1) for details. Implies --dry-run.

--long