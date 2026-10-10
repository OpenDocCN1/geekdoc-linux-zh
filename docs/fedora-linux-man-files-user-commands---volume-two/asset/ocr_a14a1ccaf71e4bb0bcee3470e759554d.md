When doing a dry-run, give the output in a the long-format. Implies —dry-run.

-z, —null

When showing short or porcelain status output, terminate entries in the status output with NUL, instead of LF. If no format is given, implies the —porcelain output format.

-F <file>, —file=<file>

Take the commit message from the given file. Use - to read the message from the standard input.

—author=<author>

Override the commit author. Specify an explicit author using the standard A U Thor <> format. Otherwise <author> is assumed to be a pattern and is used to search for an existing commit by that author (i.e. rev-list --all -i --author=<author>); the commit author is then copied from the first such commit found.

—date=<date>

Override the author date used in the commit.

-m <msg>, —message=<msg>

Use the given <msg> as the commit message. If multiple -m options are given, their values are concatenated as separate paragraphs.

-t <file>, —template=<file>

When editing the commit message, start the editor with the contents in the given file. The commit.template configuration variable is often used to give this option implicitly to the command. This mechanism can be used by projects that want to guide participants with some hints on what to write in the message in what order. If the user exits the editor without editing the message, the commit is aborted. This has no effect when a message is given by other means, e.g. with the -m or -F options.

-s, —signoff

Add Signed-off-by line by the committer at the end of the commit log message.

-n, —no-verify

This option bypasses the pre-commit and commit-msg hooks. See also (5).

—allow-empty

Usually recording a commit that has the exact same tree as its sole parent commit is a mistake, and the command prevents you from making such a commit. This option bypasses the safety, and is primarily for use by foreign SCM interface scripts.

—allow-empty-message

Like —allow-empty this command is primarily for use by foreign SCM interface scripts. It allows you to create a commit with an empty commit message without