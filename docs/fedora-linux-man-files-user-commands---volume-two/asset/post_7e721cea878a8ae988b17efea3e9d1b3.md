
file's size are eligible for being picked up as a possible source of a rename to another file.

- -M[<n>], --find-renames[=<n>]
Detect renames. If n is specified, it is a threshold on the similarity index (i.e. amount of addition/deletions compared to the file's size). For example, -M90% means Git should consider a delete/add pair to be a rename if more than 90% of the file hasn't changed. Without a % sign, the number is to be read as a fraction, with a decimal point before it. I.e., -M5 becomes 0.5, and is thus the same as -M50%. Similarly, -M05 is the same as -M5%. To limit detection to exact renames, use -M100%. The default similarity index is 50%.

- -C[<n>], --find-copies[=<n>]
Detect copies as well as renames. See also --find-copies-harder. If n is specified, it has the same meaning as for -M<n>.

- --find-copies-harder
For performance reasons, by default, -C option finds copies only if the original file of the copy was modified in the same changeset. This flag makes the command inspect unmodified files as candidates for the source of copy. This is a very expensive operation for large projects, so use it with caution. Giving more than one -C option has the same effect.

- -D, --irreversible-delete
Omit the preimage for deletes, i.e. print only the header but not the diff between the preimage and /dev/null. The resulting patch is not meant to be applied with patch or git apply; this is solely for people who want to just concentrate on reviewing the text after the change. In addition, the output obviously lack enough information to apply such a patch in reverse, even manually, hence the name of the option.

When used together with -B, omit also the preimage in the deletion part of a delete/create pair.

- -l<num>
The -M and -C options require O(n^2) processing time where n is the number of potential rename/copy targets. This option prevents rename/copy detection from running if the number of rename/copy targets exceeds the specified number.

- -O<orderfile>
Output the patch in the order specified in the <orderfile>, which has one shell glob pattern per line. This overrides the diff.orderFile configuration variable (see [1]). To cancel diff.orderFile, use -O/dev/null.

- -a, --text
Treat all files as text.

- --ignore-space-at-eol
Ignore changes in whitespace at EOL.

- -b, --ignore-space-change
Ignore changes in amount of whitespace. This ignores whitespace at line end, and considers all other sequences of one or more whitespace characters to be equivalent.

- -w, --ignore-all-space
Ignore whitespace when comparing lines. This ignores differences even if one line has whitespace where the other line has none.

- --ignore-blank-lines
Ignore changes whose lines are all blank.

- --inter-hunk-context=<lines>
Show the context between diff hunks, up to the specified number of lines, thereby fusing hunks that are close to each other.

- -W, --function-context
Show whole surrounding functions of changes.

- --ext-diff
Allow an external diff helper to be executed. If you set an external diff driver with (5), you need to use this option with (1) and friends.

- --no-ext-diff
Disallow external diff drivers.

- --textconv, --no-textconv
Allow (or disallow) external text conversion filters to be run when comparing binary files. See (5) for details. Because textconv filters are typically a one-way conversion, the resulting diff is suitable for human consumption, but cannot be applied. For this reason, textconv filters are enabled by default only for (1) and (1), but not for (1) or diff plumbing commands.

- --ignore-submodules[=<when>]
Ignore changes to submodules in the diff generation. <when> can be either "none", "untracked", "dirty" or "all", which is the default. Using "none" will consider the submodule modified when it either contains untracked or modified files or its HEAD differs from the commit recorded in the superproject and can be used to override any settings of the ignore option in (1) or (5). When "untracked" is used submodules are not considered dirty when they only contain untracked content (but they are still scanned for modified content). Using "dirty" ignores all changes to the work tree of submodules, only changes to the commits stored in the superproject are shown (this was the behavior until 1.7.0). Using "all" hides all changes to submodules.

- --src-prefix=<prefix>
Show the given source prefix instead of "a/".

- --dst-prefix=<prefix>
Show the given destination prefix instead of "b/".

- --no-prefix
Do not show any source or destination prefix.

For more detailed explanation on these common options, see also (7).

- -<n>
Prepare patches from the topmost <n> commits.

- -o <dir>, --output-directory <dir>
Use <dir> to store the resulting files, instead of the current working directory.

- -n, --numbered
Name output in [PATCH n/m] format, even with a single patch.

- -N, --no-numbered
Name output in [PATCH] format.

- --start-number <n>
Start numbering the patches at <n> instead of 1.

- --numbered-files
Output file names will be a simple number sequence without the default first line of the commit appended.

- -k, --keep-subject
Do not strip/add [PATCH] from the first line of the commit log message.

- -s, --signoff
Add Signed-off-by: line to the commit message, using the committer identity of yourself.

- --stdout
Print all commits to the standard output in mbox format, instead of creating a file for each one.

- --attach[<=<boundary>]
Create multipart/mixed attachment, the first part of which is the commit message and the patch itself in the second part, with Content-Disposition: attachment.

- --no-attach
Disable the creation of an attachment, overriding the configuration setting.

- --inline[=<boundary>]
Create multipart/mixed attachment, the first part of which is the commit message and the patch itself in the second part, with Content-Disposition: inline.

- --thread[=<style>], --no-thread
Controls addition of In-Reply-To and References headers to make the second and subsequent mails appear as replies to the first. Also controls generation of the Message-Id header to reference.

The optional <style> argument can be either *shallow* or *deep*. *shallow* threading makes every mail a reply to the head of the series, where the head is chosen from the cover letter, the --in-reply-to, and the first patch mail, in this order. *deep* threading makes every mail a reply to the previous one.

The default is --no-thread, unless the *format.thread* configuration is set. If --thread is specified without a style, it defaults to the style specified by *format.thread* if any, or else *shallow*.

Beware that the default for *git send-email* is to thread emails itself. If you want git format-patch to take care of threading, you will want to ensure that threading is disabled for git send-email.

- --in-reply-to=Message-Id
Make the first mail (or all the mails with --no-thread) appear as a reply to the given Message-Id, which avoids breaking threads to provide a new patch series.

- --ignore-if-in-upstream
Do not include a patch that matches a commit in <until>..<since>. This will examine all patches reachable from <since> but not from <until> and compare them with the patches being generated, and any patch that matches is ignored.

- --subject-prefix=<Subject-Prefix>
Instead of the standard *[PATCH]* prefix in the subject line, instead use *\[<Subject-Prefix>]*. This allows for useful naming of a patch series, and can be combined with the --numbered option.

- -v <n>, --reroll-count=<n>
Mark the series as the <n>-th iteration of the topic. The output filenames have v<n> prepended to them, and the subject prefix ("PATCH" by default, but configurable via the --subject-prefix option) has 'v<n>' appended to it. E.g. --reroll-count=4 may produce v4-0001-add-makefile.patch file that has "Subject: [PATCH v4 1/20] Add makefile" in it.

- --to=<email>
Add a To: header to the email headers. This is in addition to any configured headers, and may be used multiple times. The negated form --no-to discards all To: headers added so far (from config or command line).

- --cc=<email>
Add a Cc: header to the email headers. This is in addition to any configured headers, and may be used multiple times. The negated form --no-cc discards all Cc: headers added so far (from config or command line).

- --from, --from=<ident>
Use ident in the From: header of each commit email. If the author ident of the commit is not textually identical to the provided ident, place a From: header in the body of the message with the original author. If no ident is given, use the committer ident.

Note that this option is only useful if you are actually sending the emails and want to identify yourself as the sender, but retain the original author (and git am will correctly pick up the in-body header). Note also that git send-email already handles this transformation for you, and this option should not be used if you are feeding the result to git send-email.

- --add-header=<header>
Add an arbitrary header to the email headers. This is in addition to any configured headers, and may be used multiple times. For example, --add-header="Organization: git-foo". The negated form --no-add-header discards **all** (To:, Cc:, and custom) headers added so far from config or command line.

- --[no-]cover-letter
In addition to the patches, generate a cover letter file containing the shortlog and the overall diffstat. You can fill in a description in the file before sending it out.

- --notes[=<ref>]
Append the notes (see (1)) for the commit after the three-dash line.

The expected use case of this is to write supporting explanation for the commit that does not belong to the commit log message proper, and include it with the patch submission. While one can simply write these explanations after format-patch has run but before sending, keeping them as Git notes allows them to be maintained between versions of the patch series (but see the discussion of the notes.rewrite configuration options in (1) to use this workflow).

- --[no-]signature=<signature>
Add a signature to each message produced. Per RFC 3676 the signature is separated from the body by a line with '--' on it. If the signature option is omitted the signature defaults to the Git version number.

- --signature-file=<file>
