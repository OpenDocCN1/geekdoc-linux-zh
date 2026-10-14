The info program reads info files, which are tree-structured into individual nodes, each containing a single topic. Info files contain hyperlinks that can move you from node to node. A hyperlink can be identified by its leading asterisk and is activated by placing the cursor upon it and pressing the ENTER key.

To invoke info, enter info followed optionally by the name of a program. Table 5-2 lists commands used to control the reader while displaying an info page.

# Table 5-2: info Commands

| Command | Action |
|---|---|
| ? | Display command help. |
| PAGE UP or BACKSPACE | Display previous page. |
| PAGE DOWN or Spacebar | Display next page. |
| n | Next—Display the next node. |
| p | Previous—Display the previous node. |
| u | Up—Display the parent node of the currently displayed node, usually a menu. |
| ENTER | Follow the hyperlink at the cursor location. |
| q | Quit. |

Most of the command-line programs we have discussed so far are part of the GNU Project’s coreutils package, so you can find more information about them by typing

```
[me@linuxbox ~]$ info coreutils
```

which will display a menu page containing hyperlinks to documentation for each program provided by the coreutils package.

# README and Other Program Documentation Files

Many software packages installed on your system have documentation files residing in the /usr/share/doc directory. Most of these are stored in plaintext format and can be viewed with less. Some of the files are in HTML format and can be viewed with a web browser. We may encounter some files ending with a .gz extension. This indicates that they have been compressed with the gzip compression program. The gzip package includes a special version of less called zless, which will display the contents of gzip-compressed text files.