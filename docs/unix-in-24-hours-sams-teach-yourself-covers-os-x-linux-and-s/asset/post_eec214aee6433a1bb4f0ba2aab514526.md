
Adding the `-F` flag to `ls` appends suffixes to certain filenames so that you can ascertain more easily what types of files they are. Three different suffixes can be added, as shown in [Table 4.1](#table-4-1).

### TABLE 4.1 Filename Suffixes Appended by `ls -F`

| Suffix | Example | Meaning |
|---|---|---|
| `/` | `Mail/` | `Mail` is a directory. |
| `*` | `prog*` | `prog` is an executable program. |
| `@` | `bin@` | `bin` is a symbolic link to another file or directory. |

- 7. Mac and Windows users can both create aliases, separate files that do not contain information but act instead as pointers to the actual target files. Aliases can exist either for specific files or for folders. Windows folk might also know such a file as a “shortcut” file.

Unix has offered a similar feature forever, which in Unix jargon is called a *symbolic link*. A symbolic link, such as `bin` in [Table 4.1](#table-4-1), contains the name of another file or directory rather than any contents of its own. If you could peek inside, it might look like `bin = @/usr/bin`. Every time someone tries to look at `bin`, the system shows the contents of `/usr/bin` instead.

You’ll learn more about symbolic links and how they help you organize your files in [Hour 6, “Creating, Moving, Renaming, and Deleting Files and Directories.”](#hour-6) For now, just remember that if you see an `@` after a filename, it’s a link to another spot in the file system.

- 8. A useful flag for `ls` (one that might not be available in your version of Unix) is the `-m` flag. This flag outputs the files as a comma-separated list. If there are many files, using `-m` can be a quick and easy way to see what’s available:

[Click here to view code image](#code-image)

```
% ls -m
Archives, InfoWorld, LISTS, Mail, News, OWL, RUMORS.18Sept,
bin, lecc.list, mailing.lists, newels, src
```

Sometimes you might want to list each of your files on a separate line, perhaps for a printout you want to annotate. You’ve learned that the `-C` flag forces recalcitrant versions of `ls` to output in multiple columns. Unfortunately, the opposite behavior isn’t obtained by use of a lowercase `c`. (Unix should be so consistent!) Instead, use the `-1` flag to indicate that you want one column of output. Try it.

### Task 4.3: Combining Flags

The different flags you’ve learned so far are summarized in [Table 4.2](#table-4-2).

### TABLE 4.2 Some Useful Flags to ls

| Flag | Meaning |
|------|---------|
| -a | List all files, including any dot files. |
| -F | Indicate file types: / = directory and * = executable. |
| -m | Show files as a comma-separated list. |
| -s | Show size of files, in blocks (typically, 1 block = 1,024 bytes). |
| -C | Force multiple-column output on listings. |
| -1 | Force single-column output on listings. |
| -l | Show long-listing format, including permissions, ownership, size, and date. |

What if you want a list, generated with the -F conventions, that simultaneously shows you all files and indicates their types?

- 1. Combining flags in Unix is easy. All you have to do is run them together in a sequence of characters and prefix the whole thing with a dash:

[Click here to view code image](#code-image)

```
$ ls -aF
./      .gopherrc      .oldnewsrc      .sig
../     .history*      .plan           Archives/
Agenda  .info          .pnews expert   InfoWorld/
.aconfigrc .letter      .report         LISTS
.article .login        .rm-timestamp   Mail/
.cshrc   .mailrc        .rnlast         News/
.elm/    .newsrc        .rnsoft         OWL/
```

- 2. Sometimes it’s more convenient to keep all the flags separate. This is fine, as long as each flag is prefixed by its own dash:

[Click here to view code image](#code-image)

```
$ ls -s -F
total 403
1 Archives/   1 Mail/   5 RUMORS.18Sept   280 mailing.lists
1 InfoWorld/  1 News/   1 bin/            2 newels
261 LISTS     1 OWL/    4 iecc.list       1 src/
```

- 3. Try some of these combinations on your own computer. Also try to list a flag more than once (for example, ls -sss -s) or list flags in different orders.

Very few Unix commands care about the order in which flags are listed. Because it’s the presence or absence of a flag that’s important, listing a flag more than once also doesn’t make any difference.

### Task 4.4: Listing Other Directories Without Changing Location

Every time I try to do any research in the library, I find myself spending hours and hours there, but it seems to me that I do less research than I think I should. That’s because most of my time is for the tasks between the specifics of my research: finding the location of the next book and finding the book itself.

If ls constrained you to listing only the directory you were in, it would hobble you in a
