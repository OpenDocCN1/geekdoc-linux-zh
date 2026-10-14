# 8.2.4 Finding Files in a Directory Tree by Owner

To find files owned by a particular user, give the username to search for as an argument to the `-user` option.

+   - To list all files in the `/usr/local/fonts` directory tree owned by the user warwick, type:

```
$ find /usr/local/fonts -user warwick RET
```

The `-group` option is similar, but it matches group ownership instead of user ownership.

To list all of the files in your home directory tree that were modified from two to four days ago, type:

```
$ find ~ -mtime 2 -mtime -4 -daystart RET
```

In the preceding example, the combined options `-mtime 2` and `-mtime -4` matched files that were modified between two and four days ago.

To find files newer than a given file, give the name of that file as an argument to the `-newer` option.

+   - To find files in the `/etc` directory tree that are newer than the file `/etc/motd`, type:

```
$ find /etc -newer /etc/motd RET
```

To find files newer than a given date, use the trick described in the find Info documentation: create a temporary file in `/tmp` with touch whose timestamp is set to the date you want to search for, and then specify that temporary file as the argument to `-newer`.

+   - To list all files in your home directory tree that were modified after May 4 of the current year, type:

```
$ touch -t 05040000 /tmp/timestamp RET
$ find ~ -newer /tmp/timestamp RET
```

In this example, a temporary file called `/tmp/timestamp` is written; after the search, you can remove it (see section Removing Files and Directories).

> NOTE: You can also find files that were last accessed a number of days after they were modified by giving that number as an argument to the `-used` option. This is useful for finding files that get little use—files matching `-used +100`, say, were accessed 100 or more days after they were last modified.