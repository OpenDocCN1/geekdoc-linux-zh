# ed, red

# 299

+   2 Merry merry king of the bush is he
3 Laugh, kookaburra, laugh
4 Gay your life must be.
56 Kookaburra sits in the old gum tree
7 Eating all the gumdrops he can see
8 Laugh, kookaburra, laugh
9 Leave some there for me.

To delete a line of text, use the d (delete) command. In the following example, we delete the fifth line that contains just a new character and then the n command again to display the contents of the buffer. As you can see, the blank line has been deleted.

5d
1,$

+   1 Kookaburra sits in the old gum tree
2 Merry merry king of the bush is he
3 Laugh, kookaburra, laugh
4 Gay your life must be.
5 Kookaburra sits in the old gum tree
6 Eating all the gumdrops he can see
7 Laugh, kookaburra, laugh
8 Leave some there for me.

Now we decide to quit the file, but we've forgotten to write the changes in the buffer. ed displays a ? prompt to remind us that we haven't saved the changes. We then write the changes and quit again.

```
Q
w
?
239
Q
castle%
```

# Usage

See largefile(5) for the description of the behavior of ed and red when encountering files greater than or equal to 2 Gbytes(**31 bytes).

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of ed: HOME, LC_TYPE, LC_COLLATE, LC_MESSAGES, and NLPATH.

# Exit Status

```
0 Successful completion without any file or command errors.
>0 An error occurred.
```

# Files

```
$TMPDIR If this environment variable is not null, use its value in place of /var/tmp as the directory name for the temporary work file.
```