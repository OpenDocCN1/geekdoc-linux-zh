
...abbrev are used, and *parents* information show the true parent commits, without taking grafts or history simplification into account. Note that this format affects the way commits are displayed, but not the way the diff is shown e.g. with `git log --raw`. To get full object names in a raw diff format, use `--no-abbrev`.

*format:*<string>

The *format:*<string> format allows you to specify which information you want to show. It works a little bit like printf format, with the notable exception that you get a newline with %*n* instead of \n.

E.g. *format:*“*The author of %h was %an, %ar%n*The *title* was >>%s<<%n*” would show something like this:

The author of fe6e0ee was Junio C Hamano, 23 hours ago The title was >>t4119: test autoconputing -p<n> for traditional diff input.<<

The placeholders are:

- %*H*: commit hash
- %*h*: abbreviated commit hash
- %*T*: tree hash
- %*t*: abbreviated tree hash
- %*P*: parent hashes
- %*p*: abbreviated parent hashes
- %*an*: author name
- %*a*N: author name (respecting .mailmap, see (1) or (1))
- %*ae*: author email
- %*a*E: author email (respecting .mailmap, see (1) or (1))
- %*ad*: author date (format respects `--date=` option)
- %*a*D: author date, RFC822 style
- %*ar*: author date, relative
- %*at*: author date, UNIX timestamp
- %*ai*: author date, ISO 8601-like format
- %*a*I: author date, strict ISO 8601 format
- %*cn*: committer name
- %*c*N: committer name (respecting .mailmap, see (1) or (1))
- %*ce*: committer email
- %*c*E: committer email (respecting .mailmap, see (1) or (1))
- %*cd*: committer date (format respects `--date=` option)
- %*c*D: committer date, RFC2822 style
- %*cr*: committer date, relative
- %*ct*: committer date, UNIX timestamp
- %*ci*: committer date, ISO 8601-like format
- %*c*I: committer date, strict ISO 8601 format
- %*d*: ref names, like the --decorate option of (1)
- %*D*: ref names without the "(", ")" wrapping.
- %*e*: encoding
- %*s*: subject
- %*f*: sanitized subject line, suitable for a filename
- %*b*: body
- %*B*: raw body (unwrapped subject and body)
- %*N*: commit notes
- %*GG*: raw verification message from GPG for a signed commit
- %*G?*: show "G" for a Good signature, "B" for a Bad signature, "U" for a good, untrusted signature and "N" for no signature
- %*GS*: show the name of the signer for a signed commit
- %*GK*: show the key used to sign a signed commit
- %*gD*: reflog selector, e.g., refs/stash@{1}
- %*gd*: shortened reflog selector, e.g., stash@{1}
- %*gn*: reflog identity name
- %*gN*: reflog identity name (respecting .mailmap, see (1) or (1))
- %*ge*: reflog identity email
- %*gE*: reflog identity email (respecting .mailmap, see (1) or (1))
- %*gs*: reflog subject
- %*C*red: switch color to red
- %*C*green: switch color to green
- %*C*blue: switch color to blue
- %*C*reset: reset color
- %*C*(...): color specification, as described in color.branch.* config option; adding auto, at the beginning will emit color only when colors are enabled for log output (by color.diff, color.ui, or --color, and respecting the auto settings of the former if we are going to a terminal). auto alone (i.e. %C(auto)) will turn on auto coloring on the next placeholders until the color is switched again.
- %*m*: left, right or boundary mark
- %*n*: newline
- %*: a raw %
- %x00: print a byte from a hex code
- %w([<w> [, <i1> [, <i2>]]]): switch line wrapping, like the -w option of (1).
- %<(<N> [,trunc [ltrunc|mtrunc]]): make the next placeholder take at least N columns, padding spaces on the right if necessary. Optionally truncate at the beginning (ltrunc), the middle (mtrunc) or the end (trunc) if the output is longer than N columns. Note that truncating only works correctly with N >= 2.
- %<[(<N>): make the next placeholder take at least until Nth columns, padding spaces on the right if necessary
- %>(<N>), %>|[<N>): similar to %<(<N>), %<[(<N>) respectively, but padding spaces on the left
- %>>(<N>), %>>[(<N>): similar to %>(<N>), %>|[<N>) respectively, except that if the next placeholder takes more spaces than given and there are spaces on its left, use those spaces
- %><(<N>), %><[(<N>): similar to %<(<N>), %<[(<N>) respectively, but padding both sides (i.e. the text is centered)

### Note

Some placeholders may depend on other options given to the revision traversal engine. For example, the %g* reflog options will insert an empty string unless we are traversing reflog entries (e.g., by git log -g). The %d and %D placeholders will use the “short” decoration format if --decorate was not already provided on the command line.

If you add a + (plus sign) after % of a placeholder, a line-feed is inserted immediately before the expansion if and only if the placeholder expands to a non-empty string.

If you add a - (minus sign) after % of a placeholder, line-feeds that immediately precede the expansion are deleted if and only if the placeholder expands to an empty string.

If you add a ` ` (space) after % of a placeholder, a space is inserted immediately before the expansion if and only if the placeholder expands to a non-empty string.

*tformat*:

The *tformat:* format works exactly like *format:*; except that it provides “terminator” semantics instead of “separator” semantics. In other words, each commit has the message terminator character (usually a newline) appended, rather than a separator placed between entries. This means that the final entry of a single-line format will be properly terminated with a new line, just as the “oneline” format does. For example:

```
$ git log -2 --pretty=format:%h 4da45bef \
| perl -pe '$_ .= "—NO\n' unless /^\n/'
4da45be 7134973—NO NEWLINE
$ git log -2 --pretty=tformat:%h 4da45bef \
| perl -pe '$_ .= "—NO NEWLINE\n' unless /^\n/'
4da45be 7134973
```

In addition, any unrecognized string that has a % in it is interpreted as if it has format: in front of it. For example, these two are equivalent:

```
$ git log -2 --pretty=tformat:%h 4da45bef
$ git log -2 --pretty=%h\n4da45bef
```

## LIMITING OUTPUT

If you’re only interested in differences in a subset of files, for example some architecture-specific files, you might do:

```
git diff-tree -r <tree-ish> <tree-ish> arch/ia64 include/asm-ia64
```

and it will only show you what changed in those two directories.

Or if you are searching for what changed in just kernel/sched.c, just do

```
git diff-tree -r <tree-ish> <tree-ish> kernel/sched.c
```

and it will ignore all differences to other files.

The pattern is always the prefix, and is matched exactly. There are no wildcards. Even stricter, it has to match a complete path component. I.e. “foo” does not pick up foo/bar.h. “foo” does match foo/bar.h so it can be used to name subdirectories.

An example of normal usage is:

```
~/git> git diff-tree --abbrev 5319e4 :100664 100664 ac348b… a01513…  git-fsck-objects.c
```

which tells you that the last commit changed just one file (it’s from this one:

```
commit 3c6f7ca19ad4043e9e72fa94106f352897e651a8
tree 5319e4d609ccdd282069cc4dce33c1db559539b03
parent b4e628ea30d5ab3606119d2ea5caea b141d38df7
author Linus Torvalds <torvalds@linux-foundation.org> Sat Apr 9 12:02:30 2005
committer Linus Torvalds <torvalds@linux-foundation.org> Sat Apr 9 12:02:30 2005

    Make "git-fsck-objects" print out all the root commits it finds.
    Once I do the reference tracking, I’ll also make it print out all the
    HEAD commits it finds, which is even more interesting.
```

in case you care).

## RAW OUTPUT FORMAT

The raw output format from “git-diff-index”, “git-diff-tree”, “git-diff-files” and “git diff —raw” are very similar.

These commands all compare two sets of things; what is compared differs:

```
git-diff-index <tree-ish>
```

compares the <tree-ish> and the files on the filesystem.

```
git-diff-index --cached <tree-ish>
```

compares the <tree-ish> and the index.

```
git-diff-tree [-r] <tree-ish-1> <tree-ish-2> [pattern>…]
```

compares the trees named by the two arguments.

```
git-diff-files [<pattern>…]
```

compares the index and the files on the filesystem.

The “git-diff-tree” command begins its output by printing the hash of what is being compared. After that, all the commands print one output line per changed file.

An output line is formatted this way:

```
in-place edit   :100644 100644 bcd1234…  0123456…  M   file0
copy-edit       :100644 100644 abcd123…  1234567…  C68 file1 file2
rename-edit     :100644 100644 abcd123…  1234567…  R86 file1 file3
create          :000000 100644 0000000…  1234567…  A   file4
delete          :100644 000000 1234567…  0000000…  D   file5
unmerged        :000000 000000 0000000…  0000000…  U   file6
```

That is, from the left to the right:

1. a colon.
2. mode for “src”; 000000 if creation or unmerged.
3. a space.
4. mode for “dst”; 000000 if deletion or unmerged.
5. a space.
6. sha1 for “src”; 0{40} if creation or unmerged.
7. a space.
8. sha1 for “dst”; 0{40} if creation, unmerged or “look at work tree”.
9. a space.
10. status, followed by optional “score” number.
11. a tab or a NUL when -z option is used.
12. path for “src”
