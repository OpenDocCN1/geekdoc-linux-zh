+   —perl-regexp
+       Consider the limiting patterns to be Perl-compatible regular expressions. Requires libcore to be compiled in.

+   —remove-empty
+       Stop when a given path disappears from the tree.

+   —merges
+       Print only merge commits. This is exactly the same as —min-parents=2.

+   —no-merges
+       Do not print commits with more than one parent. This is exactly the same as —max-parents=1.

+   —min-parents=<number>，—max-parents=<number>，—no-min-parents，—no-max-parents
+       Show only commits which have at least (or at most) that many parent commits. In particular，—max-parents=1 is the same as —no-merges，—min-parents=2 is the same as —merges. —max-parents=0 gives all root commits and —min-parents=3 all octopus merges.
+       —no-min-parents and —no-max-parents reset these limits (to no limit) again. Equivalent forms are —min-parents=0 (any commit has 0 or more parents) and —max-parents=-1 (negative numbers denote no upper limit).

+   —first-parent
+       Follow only the first parent commit upon seeing a merge commit. This option can give a better overview when viewing the evolution of a particular topic branch, because merges into a topic branch tend to be only about adjusting to updated upstream from time to time, and this option allows you to ignore the individual commits brought in to your history by such a merge. Cannot be combined with —bisect.

+   —not
+       Reverses the meaning of the ^ prefix (or lack thereof) for all following revision specifiers, up to the next —not.

+   —all
+       Pretend as if all the refs in refs/ are listed on the command line as <commit>.

+   —branches[=<pattern>]
+       Pretend as if all the refs in refs/heads are listed on the command line as <commit>. If <pattern> is given, limit branches to ones matching given shell glob. If pattern lacks ?, *, or [,* at the end is implied.

+   —tags[=<pattern>]