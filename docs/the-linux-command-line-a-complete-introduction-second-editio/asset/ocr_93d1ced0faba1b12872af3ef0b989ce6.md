| Command | Action |
|---|---|
| n | Next—display the next node |
| p | Previous—display the previous node |
| U | Up—display the parent node of the currently displayed node, usually a menu |
| ENTER | Follow the hyperlink at the cursor location |
| Q | Quit |

Most of the command line programs we have discussed so far are part of the GNU Project's coreutils package, so typing the following:

```
[me@linuxbox ~]$ info coreutils
```

will display a menu page with hyperlinks to each program contained in the coreutils package.

# README and Other Program Documentation Files

Many software packages installed on your system have documentation files residing in the /usr/share/doc directory. Most of these are stored in ordinary text format and can be viewed with the less command. Some of the files are in HTML format and can be viewed with a web browser. We may encounter some files ending with a .gz extension. This indicates that they have been compressed with the gzip compression program. The gzip package includes a special version of less called zless that will display the contents of gzip-compressed text files.

# Creating Our Own Commands with alias

Now for our first experience with programming! We will create a command of our own using the alias command. But before we start, we need to reveal a small command line trick. It's possible to put more than one command on a line by separating each command with a semicolon. It works like this: