
The `-regex` option matches the whole path name, relative to the directory tree you specify, and not just file names; for this reason, the regexps in the previous examples began with `.*`, so that characters making up the path were matched first. To only match file names in a search for a word or phrase, exclude the forward slash character (`/`) after the string you’re searching for, and exclude directory names with `! -type d` (see Recipe 7.4.5 [Finding the Number of Files in a Listing], page 184).

⇒ To list all files in the current directory tree whose names have either the string `net` or `comm` anywhere in their file names, type:

```
$ find . -regex '.*\(net\|comm\)\./.*' ! -type d [RET]
```

## 7.2.2 Finding Files in a Directory Tree by Size

To find files of a certain size, use the `-size` option, following it with the file size to match. The default unit is 512-byte blocks; follow the size with `k` to denote kilobytes or `b` to denote bytes.

⇒ Here are some ways to use this.

- To list all files in the `/usr/local` directory tree that are greater than 10,000 kilobytes in size, type:

```
$ find /usr/local -size +10000k [RET]
```

- To list all files in your home directory tree less than 300 bytes in size, type:

```
$ find ~ -size -300b [RET]
```

- To list all files on the system whose size is exactly 42 512-byte blocks, type:

```
$ find / -size 42 [RET]
```

Use the `-empty` option to find empty files—files whose size is 0 bytes. This is useful for finding files that you might not need, and can remove.

⇒ To find all empty files in your home directory tree, type:

```
$ find ~ -empty [RET]
```

NOTES: To find the largest or smallest files in a given directory, output a sorted listing of that directory (see Recipe 7.4 [Finding Files in Directory Listings], page 182).

## 7.2.3 Finding Files in a Directory Tree by Access Time

To find files that were last accessed during a specified time, use `find` with any of the `-amin`, `-anewer`, or `-atime` options. The argument you give with `-amin` specifies the number of minutes ago that the file was accessed; you can also find files that were accessed more recently than the file name given as an argument to `-anewer` was modified. Finally, `-atime` specifies the number of 24-hour periods ago when the file was last accessed.

⇒ Here are some ways to use this.

- To find all files in your home directory tree that were last accessed one hour ago, type:

```
$ find ~ -amin 60 [RET]
```

- To find all files in your home directory tree that were last accessed within the past sixty minutes, type:

```
$ find ~ -amin -60 [RET]
```

- To find all files in the `/usr/share` directory tree that were last accessed twenty-four hours ago, type:

```
$ find /usr/share -atime 1 [RET]
```

- To find all files in the `/usr/share` directory tree that were last accessed more recently than the file `/template` was modified, type:

```
$ find /usr/share -anewer /template [RET]
```

Include the `-daystart` option to measure time from the beginning of the current day, instead of 24 hours ago. This option must precede the time expression it works on.

⇒ To find all files in the `/usr/share` directory tree that were last accessed two days ago, type:

```
$ find /usr/share -daystart -atime 2 [RET]
```

## 7.2.4 Finding Files in a Directory Tree by Change Time

To find files whose status last changed at a specified time (that is, its permissions and not its contents), use `find` with the `-ctime`, `-cmin`, or `-cnewer` options; the argument you give with `-ctime` specifies the number of 24-hour periods, and with `-cmin` it specifies the number of minutes. A file name given as an argument to `-anewer` specifies files whose status have changed more recently than this particular file was modified.

⇒ Here are some ways to use this.

- To find all files in your home directory tree whose status has changed within the last ten minutes, type:

```
$ find ~ -cmin -10 [RET]
```

- To find all the files on the system whose status has changed more recently than the file `/etc/inittab` was modified, type:

```
$ find / -cnewer /etc/inittab [RET]
```

- To find all files in the current directory tree whose status last changed exactly twenty-four hours ago, type:

```
$ find . -ctime 1 [RET]
```

- To find all files in the current directory tree whose status has changed within the last twenty-four hours, type:

```
$ find . -ctime -1 [RET]
```

Include the `-daystart` option to measure time from the beginning of the current day, instead of 24 hours ago. This option must precede the time expression it works on.

⇒ To find all files in the current directory tree whose status last changed a week ago, type:

```
$ find . -daystart -ctime 7 [RET]
```

## 7.2.5 Finding Files in a Directory Tree by Modification Time

To find files last modified at a specified time, use `find` with the `-mtime` or `-mmin` options; the argument you give with `-mtime` specifies the number of 24-hour periods, and with `-mmin` it specifies the number of minutes.

⇒ Here are some ways to use this.

- To list all the files in the current directory tree whose contents have been modified within the last ten minutes, type:

```
$ find . -mmin -10 [RET]
```

- To list the files in the `/usr/local` directory tree that were modified exactly 24 hours ago, type:

```
$ find /usr/local -mtime 1 [RET]
```

- To list the files in the `/usr` directory tree that were modified exactly five minutes ago, type:

```
$ find /usr -mmin 5 [RET]
```

- To list the files in the `/usr/local` directory tree that were modified within the past 24 hours, type:

```
$ find /usr/local -mtime -1 [RET]
```
