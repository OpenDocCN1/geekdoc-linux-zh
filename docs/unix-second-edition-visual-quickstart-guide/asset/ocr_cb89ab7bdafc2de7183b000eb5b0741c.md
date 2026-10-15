# Changing Files with awk

While sed is line-oriented and lets you fiddle and diddle to your heart’s content, awk is field-oriented and is ideal for manipulating database or comma-delimited files. For example, if you have an address book file, you can use awk to find and change information in fields you specify, as in Code Listing 6.11. In the following steps, we’ll show you a sampling of the things you can do using awk to modify, in this example, an address book file.

# To change files with awk:

+   1. awk '{ print $1 }' address.book
+   At the shell prompt, use awk '{ print $1 }' address.book file to look at the address.book file and select (and send to standard output) the first field in each record (line). More specifically, starting from the inside out

> $1 references the first field in each line. Unless you specify otherwise, awk assumes that a space separates the fields, so the first field starts at the beginning of the line and continues to the first space.

> {} contain the awk command, and the quotes are necessary to tie the awk command together (so the first space within the command isn’t interpreted by the shell as the end of the command). See Code Listing 6.11.

+   2. awk -F ', ' '{ print $1 }' address.book
+   The -F flag tells awk to use the character following it—in this case, a comma (, )—as the field separator. This change makes the output of the command a little cleaner and more accurate. If you were working with /etc/passwd, you’d use -F: to specify that the : is the field separator.

```
[ejr@hobbes manipulate]$ awk '{ print $1 }' address.book
Schmidt,
Feldman,
Brown,
Smith,
Jones,
[ejr@hobbes manipulate]$
```

Code Listing 6.11 awk lets you access individual fields in a file.

# De-what?

A delimited file uses a specific character to show where one bit of information ends and another begins. Each piece of information is a separate field. For example, a file that contains "John, Doe, Thornton, Colorado" is comma-delimited, sporting a comma between fields. Other files, such as the /etc/passwd file, use a colon (:) to separate the fields. Just about any symbol that’s not used in the content could be used as a delimiter.