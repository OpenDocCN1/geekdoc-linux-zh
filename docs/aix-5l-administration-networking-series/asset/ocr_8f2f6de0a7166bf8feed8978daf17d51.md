will display the online documentation for the **man** command. The **man** command searches and displays documents in the following order:

+   * Any **nroff** directories (**man?**) in the `/usr/share/man` directory structure.
+   * The formatted-version directories (**cat?**) in the `/usr/share/man` directory structure.
+   * If the previous two searches fail, the hypertext (DocSearch) database is searched.
+   The hypertext documentation is located in the `/usr/share/man/info` directory structure.

# Installing man Pages on AIX 4.3.3 and 5L Version 5.1

If your system only needs the man pages, then DocSearch may be overkill for you. To install the man pages on both 4.3.3 and 5L, all of the following filesets must be installed:

+   bos.html.en_US.topnav.navigate - Top Level Navigation
+   bos.html.en_US.nav - Online Navigation
+   bos.html.en_US.cmds.cmddal - AIX Commands Reference 1
+   bos.html.en_US.cmds.cmsd2 - AIX Commands Reference 2
+   bos.html.en_US.cmds.cmsd3 - AIX Commands Reference 3
+   bos.html.en_US.cmds.cmsd4 - AIX Commands Reference 4
+   bos.html.en_US.cmds.cmsd5 - AIX Commands Reference 5
+   bos.html.en_US.cmds.cmsd6 - AIX Commands Reference 6

# Using the man Pages

The **man** command has access to information stored in DocSearch. When invoked, **man** will first search `/usr/man/cat?` directories, then `/usr/man/man?`, and, finally, DocSearch data if it is installed. The commands **man** and **catman** map man page sections 1, 2, and 8 to DocSearch commands documents, sections 2 and 3 to DocSearch subroutines documents, and sections 4, 5, and 7 to DocSearch files documents. You will need to periodically execute **catman -w** to keep the database for the **arprofs** and **whatis** commands up to date.

```
# catman -w
```

From time to time, you may need to add your own custom man page information. This could be a help file explaining billing policies, backup support, locally developed software, and so on. It’s a good idea to keep local man pages separate from vendor-supplied help. This keeps them from getting stepped on during installation, maintenance, and upgrade activities. Commonly used location paths for local man pages