UNIX has offered a similar feature for many years, which in UNIX jargon is called a symbolic link. A symbolic link, such as bin in Table 4.1, contains the name of another file or directory rather than contents of its. If you could peek inside, it might look like bin = @usr/bin. Every time someone tries to look at bin, the system shows the contents of /usr/bin instead.

You'll learn more about symbolic links and how they help you organize your files a bit later in the book. For now, remember that if you see an @ filename, it's a link to another spot in the file system.

+   - A flag for ls (one that might not be available in your version of UNIX) is the -m flag outputs files as a comma-separated list. If there are many files, -m can be a quick and easy way to see what's available.

```
% ls -m
Archives, Infolist, LISTS, Mail, News, OWL, RUMORS.18Sept., bin, ie.list, mailing.lists, src
```

Sometime you might want to list each of your files on a separate line, perhaps for a printout you want to annotate. You've seen that the -c flag forces recalcitrant versions of ls to output in multiple columns. Unfortunately, the opposite behavior isn't obtained using a lowercase c. (UNIX should be so consistent!) Instead, use the -1 flag to indicate that you have one column of output. Try it.

# Task 4.3: Combining Flags

The different flags you've learned so far are summarized in Table 4.2.

Table 4.2. Some useful flags to ls.
| Flag | Meaning |
| -a | List all files, including any dot files |
| -F | Indicate file types; /= = directory, * = executable. |
| -m | Show files as a comma-separated list. |
| -s | Show size of files, in blocks (typically, 1 block = 1,024 bytes). |
| -C | Force multiple-column output on listings. |
| -1 | Force single-column output on listings. |

What you want to list a list, generated with the -F conventions, that simultaneously shows you all files and indicates their types?