This `grep` command searches for the *pattern* in the specified *files*, and *[options]* denote one or more single-character options that begin with a hyphen. Here are the options and their meanings:

+   - `-N` (where N is a number) displays N lines around the line containing the pattern.
+   - `-c` shows the number of lines that contain the search pattern.
+   - `-f` reads options from a specified file.
+   - `-i` ignores case.
+   - `-l` displays the filenames that contain the pattern.
+   - `-n` displays a line number next to lines that contain the pattern.
+   - `-q` returns a status code but does not display any output.
+   - `-v` displays the lines that do not contain a pattern.
+   - `-w` matches only whole words.

# # locate: Finding Files and Directories the Easy Way

The locate command searches a database of filenames for any name that matches a specified pattern. If you are not sure about the location of a file, just type **locate** followed by a part of the filename. For example, here’s how you can search for the rcnetwork file:

```
```bash
locate rcnetwork
```
```

This causes locate to display all file or directory names that contain `rcnetwork` in their names.

I love the locate command. I use it all the time whenever I want to check if a certain file exists somewhere in my system. Sometimes a huge number of files and directories might contain the search word. You can send the output of locate through more by typing **locate keyword | more** and browsing the output a page at a time. Another trick is to send the output through the grep command and look for some other word that helps you find a specific file. For example, when I want to see if there is a binary (executable) file with rpm in its name, I type **locate rpm | grep bin** because I know that the binary files would be in a directory whose name contains bin (for example, /bin, /usr/bin or /sbin, and so on).

The locate command isn’t installed by default in SUSE Linux.

![](bbox=[0.12, 0.873, 0.207, 0.944])