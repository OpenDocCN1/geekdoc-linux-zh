command lines. If we don’t include this line, someone running a shell other than the **ksh** might have unexpected results when trying to run one of our programs.

As a good practice, you should include `#!/shellname` as the first line of every shell program you write.

Let’s now view the next line of our program:

```
# This is a simple command file to display today's date.
```

These are comments. Everything after a `#` in a command line is considered a comment (`#!` on the first line is the one very big exception). Keep in mind my early remarks about including comments liberally. It is a great pleasure to share a well commented shell program with a friend, knowing that you have adequately documented the program with comments.

Here is the next command:

```
echo "Today's date is"
```

The **echo** command generates prompts and messages in shell programs. See the **echo** manual entry to see all the options available with **echo** for formatting your output. We commonly enclose the string to be displayed in double quotes. In this case, we did because we needed to let the shell know that the apostrophe was part of the string and not a single quote that needs a match.

Next is the last command in our program:

```
date +%x
```

This executes the **date** command. There are indeed many options to the **date** command, some of which are not intuitive. In this case, we use one of the simplest forms of the command, which simply produces today’s date.