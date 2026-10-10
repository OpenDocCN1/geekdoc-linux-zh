Suppress commit summary message.

+   —dry-run
+   	 Do not create a commit, but show a list of paths that are to be committed, paths with local changes that will be left uncommitted and paths that are untracked.

+   —status
+   	 Include the output of (1) in the commit message template when using an editor to prepare the commit message. Defaults to on, but can be used to override configuration variable commit.status.

+   —no-status
+   	 Do not include the output of (1) in the commit message template when using an editor to prepare the default commit message.

+   -S[<keyid>], —gpg-sign[=<keyid>]
+   	 GPG-sign commit.

+   —no-gpg-sign
+   	 Countermand commit.gpgSign configuration variable that is set to force each and every commit to be signed.

+   —
+   	 Do not interpret any more arguments as options.

<file>…

When files are given on the command line, the command commits the contents of the named files, without recording the changes already staged. The contents of these files are also staged for the next commit on top of what have been staged before.