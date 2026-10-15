# — Useful Commands —

The apache server needs full access to the repository:

```
# chown -R www:www /home/svn
```

Create a user with htpasswd2:

```
# htpasswd -c /etc/svn-passwd user1  # -c creates the file
```

# Access control svn.acl example

```
# Default it read access. "* =" would be default no access
[/]
* = r
[groups]
project1-developers = joe, jack, jane
# Give write access to the developers
[project1:]
@project1-developers = rw
```

# 13.2 SVN commands and usage

See also the Subversion Quick Reference Card20. Tortoise SVN21 is a nice Windows interface.

# Import

A new project, that is a directory with some files, is imported into the repository with the import command. Import is also used to add a directory with its content to an existing project.

```
# svn help import                  # Get help for any command
# Add a new directory (with content) into the src dir on project1
# svn import /project1/newdir http://host.url/svn/project1/trunk/src -m 'add newdir'
```

# Typical SVN commands

```
# svn co http://host.url/svn/project1/trunk          # Checkout the most recent version
# Tags and branches are created by copying
# svn mkdir http://host.url/svn/project1/tags/        # Create the tags directory
# svn copy -m "Tag rcl rel." http://host.url/svn/project1/trunk \ http://host.url/svn/project1/tags/1.0rc1
# svn status [--verbose]                              # Check files status into working dir
# svn add src/file.h src/file.cpp                     # Add two files
# svn commit -m 'Added new class file'                # Commit the changes with a message
# svn ls http://host.url/svn/project1/tags/           # List all tags
# svn move foo.c bar.c                                # Move (rename) files
# svn delete some_old_file                            # Delete files
```

# 14 USEFUL COMMANDS

less (p39) | vi (p40) | mail (p40) | tar (p41) | dd (p41) | screen (p42) | find (p43) | Miscellaneous (p43)

# 14.1 less

The less command displays a text document on the console. It is present on most installation.

```
# less unix toolbox.xhtml
```

Some important commands are (^N stands for [control]-[N]):

+   h H good help on display
+   f ^F ^V SPACE Forward one window (or N lines).
+   b ^B ESC-v Backward one window (or N lines).
+   F Forward forever; like "tail -f".
+   /pattern Search forward for (N-th) matching line.
+   ?pattern Search backward for (N-th) matching line.

20.http://www.cs.put.poznan.pl/csobaniec/Papers/svn-refcard.pdf
21.http://tortoisesvn.tigris.org