
So, using du we can get a printout of the size of each file in our home directory, in human-readable format, and with a summary at the end, like this:

```
du -ahc /home/paul
```

Two advanced parameters deal with filenames you want excluded from your count. The first is —exclude, which allows you to specify a pattern that should be used to exclude files. This pattern is a standard shell file matching pattern as opposed to a regular expression, which means you can use ? to match a single character or * to match 0 or many characters. You can specify multiple —exclude parameters to exclude several patterns. For example:

```
du --exclude="*.xml" --exclude="*.xsl"
```

Of course, typing numerous —exclude parameters repeatedly is a waste of time, so you can use -X to specify a file that has the list of patterns you want excluded. The file should look like this:

- *.xml
- *.xsl

That is, each pattern you want excluded should be on a line by itself. If that file were called xml_exclude.txt, we could use it in place of the previous example like this:

```
du -X xml_exclude.txt
```

You can make your exclusion file as long as you need, or you can just specify multiple -X parameters.

## TIP

> Running du in a directory where several files are hard-linked to the same inode counts the size of the file only once. If you want to count each hard link separately for some reason, use the -l parameter (lowercase L).

## Finding Files by Searching with find

The find command is one of the darkest and least understood areas of Linux, but it is also one of the most powerful. Admittedly, the find command does not help itself by using X-style parameters. The Unix standard is -c, -s, and so on, whereas the GNU standard is --dosomething, --mooby, and so forth. X-style parameters merge the two by having words preceded by only one dash.

However, the biggest problem with find is that it has more options than most people can remember—it truly is capable of doing most things you could want. The most basic usage is this:

```
find -name "*.txt"
```

That searches the current directory and all subdirectories for files that end in .txt. The previous search finds files ending in .txt but not .TXT, .Txt, or other case variations. To search without case sensitivity, use -iname instead of -name. You can optionally specify where the search should start before the -name parameter, like this:

```
find /home -name "*.txt"
```

Another useful test is -size, which lets you specify how big the files should be to match. You can specify your size in kilobytes and optionally also use + or - to specify greater than or less than. For example:

```
find /home -name "*.txt" -size 100k
```

```
find /home -name "*.txt" -size +100k
```

```
find /home -name "*.txt" -size -100k
```

The first brings up files of exactly 100KB, the second only files larger than 100KB, and the last only files under 100KB.

Moving on, the -user option enables you to specify the user who owns the files you are looking for. So, to search for all files in /home that end with .txt, are under 100KB, and are owned by user paul, you would use this:

```
find /home -name "*.txt" -size -100k -user paul
```

You can flip any of the conditions by specifying -not before them. For example, you can add a -not before -user paul to find matching files owned by everyone but paul:

```
find /home -name "*.txt" -size -100k -not -user paul
```

You can add as many -not parameters as you need, even using -not -not to cancel each other out! (Yes, that is pointless.) Keep in mind, though, that -not -size -100k is essentially equivalent to -size +100k, with the exception that the former will match files of exactly 100KB whereas the latter will not.

You can use -perm to specify which permissions a file should have for it to be matched. This is tricky, so read carefully. The permissions are specified in the same way as with the chmod command: u for user, g for group, o for others, r for read, w for write, and x for execute. However, before you give the permissions, you need to specify either a plus, a minus, or a blank space. If you specify neither a plus nor a minus, the files must exactly match the mode you give. If you specify -, the files must match all the modes you specify. If you specify +, the files must match any the modes you specify. Confused yet?

The confusion can be cleared up with some examples. This next command finds all files that have permission o=r (readable for other users). Notice that if you remove the -name parameter, it is equivalent to * because all filenames are matched.

```
find /home -perm -o=r
```
