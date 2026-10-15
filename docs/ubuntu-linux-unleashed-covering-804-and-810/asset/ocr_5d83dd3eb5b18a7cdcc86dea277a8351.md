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