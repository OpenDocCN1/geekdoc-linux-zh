
+   - To list the files in the /usr directory tree that were modified within the past five minutes, type:
+     $ find /usr -mmin -5 [RET]

Include the -daystart option to measure time from the beginning of the current day, instead of 24 hours ago. This option must precede the time expression it works on.

+   - To list all of the files in your home directory tree that were modified yesterday, type:
+     $ find ~ -daystart -mtime 1 [RET]
+   - To list all of the files in the /usr directory tree that were modified one year or longer ago, type:
+     $ find /usr -daystart -mtime +365 [RET]
+   - To list all of the files in your home directory tree that were modified from two to four days ago, type:
+     $ find ~ -daystart -daystart -mtime +2 -mtime -4 [RET]

In the preceding example, the combined options -mtime +2 and -mtime -4, each prefaced by the -daystart option, matched files that were modified between two and four days ago.

To find files newer than a given file, give the name of that file as an argument to the -newer option.

+   - To find files in the /etc directory tree that are newer than the file /etc/motd, type:
+     $ find /etc -newer /etc/motd [RET]

To find files newer than a given date, use the trick described in the find Info documentation: Create a temporary file in /tmp with touch whose timestamp is set to the date you want to search for, and then specify that temporary file as the argument to -newer.

+   - To list all files in your home directory tree that were modified after May 4 of the current year, type:
+     $ touch -t 05040000 /tmp/timestamp [RET]
+     $ find ~ -newer /tmp/timestamp [RET]

In this example, a temporary file called /tmp/timestamp is written; after the search, you can remove it (see Recipe 5.6 [Removing Files and Directories], page 149).

NOTES: You can also find files that were last accessed a number of days after they were modified by giving that number as an argument to the -used option. This is useful for finding files that get little use—files matching -used +100, say, were accessed 100 or more days after they were last modified.

## 7.2.6 Finding Files in a Directory Tree by Owner

To find files owned by a particular user, give the username to search for as an argument to the -user option.

+   ⇒ To list all files in the /usr/local/fonts directory tree owned by the user warwick, type:

```
$ find /usr/local/fonts -user warwick [RET]
```

The -group option is similar, but it matches group ownership instead of user ownership.

+   ⇒ To list all files in the /dev directory tree owned by the audio group, type:

```
$ find /dev -group audio [RET]
```

## 7.2.7 Running Commands on the Files You Find

You can also use find to execute a command you specify on each found file, by giving the command as an argument to the -exec option. If you use the string "{}" in the command, this string is replaced with the file name of the current found file when the command executes. Mark the end of the command with a semicolon character enclosed in single quotes (;).

+   ⇒ To find all files in the ~/html/ directory tree with an .html extension, and then output lines from these files that contain the string "organic," type (all on one line):

```
$ find ~/html/ -name '*.html' -exec grep organic '{}' ';' [RET]
```

In this example, the command grep organic file is executed for each file that find finds, with file being the name of each file in turn.

To have find pause and confirm execution for each file it finds, use -ok instead of -exec.

+   ⇒ To remove files from your home directory tree that were accessed more than one year after they were last modified, pausing to confirm before each removal, type:

```
$ find ~ -used +365 -ok rm '{}' ';' [RET]
```

## 7.2.8 Finding Files by Multiple Criteria

You can combine many of find's options to find files that match multiple criteria.

⇒ Here are two ways to use this.

+   - To list files in your home directory tree whose names begin with the string top, and that are newer than the file /etc/motd, type:
+     $ find ~ -name 'top*' -newer /etc/motd [RET]

+   - To compress all the files in your home directory tree that are two megabytes or larger, and that are not already compressed with gzip (having a .gz file name extension), type (all on one line):
+     $ find ~ -size +200000c -regex '.*[^.gz]' -exec gzip '{' ';' [RET]

As all options are combinable, you can use multiple calls of the same option. So you can combine several of the same time options to get a range of times, for instance.

⇒ To find all files in your home directory whose contents were modified today, but at least 120 minutes ago, type:
  $ find ~ -daystart -mtime 0 -mmin +120 [RET]

Use the special -o option (the OR operator), to separate two options when either of them are to be matched. For example, you can use it with multiple -name options to find different file names in the same directory tree.

⇒ To find all files ending in .ps, .pdf, or .dvi in the current directory tree, type (all on one line):
  $ find . -name '*.ps' -o -name '*.pdf' -o -name '*.dvi' [RET]

The following tables describe some of the many options you can use with find. The first table lists and describes find's general options for specifying its behavior.

-daystart	Use the beginning of today rather than 24 hours previous for time criteria.
-depth	Search the subdirectories before each directory.
-maxdepth levels	Specifies the maximum number of directory levels to descend in the specified directory tree.
-mount or -xdev	Do not descend directories that have another disk mounted on them.
