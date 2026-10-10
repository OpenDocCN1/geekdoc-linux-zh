successfully removes both of the leading blank lines while keeping the blank line within the data intact.

# **Deleting trailing blank lines**

Unfortunately, deleting trailing blank lines is not as simple as deleting leading blank lines. Just like printing the end of a data stream, deleting blank lines at the end of a data stream requires a little ingenuity and looping.

Before we start the discussion, let's see what the script looks like:

```
```
sed '{
:start
/^\n*$/{$d; N; b start }
}'
```
```

This may look a little odd to you at first. Notice that there are braces within the normal script braces. This allows you to group commands together within the overall command script. The group of commands applies to the specified address pattern. The address pattern matches any line that contains only a newline character. When one is found, if it's the last line, the d command deletes it. If it's not the last line, the N command appends the next line to it, and the branch (b) command loops to the beginning to start over.

Here's the script in action:

```
```
$ cat data10.txt
Line one.
Line two.
```
```

```
```
$
$ sed '{
> :start
> /^\n*$/{$d; N; b start}
> }' data10.txt
Line one.
Line two.
$ 
```
```

The script successfully removed the blank lines from the end of the