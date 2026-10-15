Any files that have o=rw set are returned from that query. Those files also might have u=rw and other permissions, but as long as they have o=rw, they will match. This next query matches all files that have o=rw set:

```
find /home -perm -o=rw
```

However, that query does not match files that are o=r or o=w. To be matched, a file must be readable and writable by other users. If you want to match readable or writeable (or both), you need to use +, like this:

```
find /home -perm +o=rw
```

Similarly, this next query matches files only that are readable by user, group, and others:

```
find /home -perm -ugo=r
```

Whereas this query matches files as long as they are readable by the user, or by the group, or by others, or by any combination of the three:

```
find /home -perm +ugo=r
```

If you use neither + or -, you are specifying the exact permissions to search for. For example, the next query searches for files that are readable by user, group, and others but not writeable or executable by anyone:

```
find /home -perm ugo=r
```

You can be as specific as you need to be with the permissions. For example, this query finds all files that are readable for the user, group, and others and writeable by the user:

```
find /home -perm ugo=r,u+w
```

To find files that are not readable by others, use the -not condition, like this:

```
find /home -not -perm +o=r
```

Now, on to the most advanced aspect of the find command: the -exec parameter. This enables you to execute an external program each time a match is made, passing in the name of the matched file wherever you want it. This has very specific syntax: Your command and its parameters should follow immediately after -exec, terminated by \;. You can insert the filename match at any point using {} (an opening and a closing brace side by side).

So, you can match all text files on the entire system (that is, searching recursively from / rather than from /home as in our previous examples) over 10KB, owned by paul, that are not readable by other users, and then use chmod to enable reading, like this:

```
find / -name "*.txt" -size +10k -user paul -not -perm +o=r -exec chmod o+r {} \;
```