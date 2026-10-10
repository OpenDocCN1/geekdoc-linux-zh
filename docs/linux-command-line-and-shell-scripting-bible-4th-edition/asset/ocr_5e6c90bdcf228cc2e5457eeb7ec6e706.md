```
[...]
Processing triggers for man-db (2.9.1-1) ...
$
$ readlink -f /usr/bin/vi
/usr/bin/vim.basic
$
```

The basic vim editor is now installed on this Ubuntu distribution, and the /usr/bin/vi program file's link was automatically changed to point to /usr/bin/vim.basic . Thus, when the vi command is entered on this Ubuntu system, the basic vim editor is used instead of tiny vim.

# ### Exploring vim basics

The vim editor works with data in a memory buffer. To start the vim editor, just type the vim command (or vi if there's an alias or linked file) and the name of the file you want to edit:

```
$ vi myprog.c
```

If you start vim without a filename, or if the file doesn't exist, vim opens a new buffer area for editing. If you specify an existing file on the command line, vim reads the entire file's contents into a buffer area, where it is ready for editing, as shown in Figure 10-1.