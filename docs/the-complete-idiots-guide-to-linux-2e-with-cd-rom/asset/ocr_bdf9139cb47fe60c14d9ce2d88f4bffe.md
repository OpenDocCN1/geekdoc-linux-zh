To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

Permissions are displayed as a series of ten dashes and/or letters at the beginning of each line.

+   - The first character position tells you about the file’s type. Regular files such as reme.txt show a dash (–) in this space. Directories such as “stuff” in the previous example show a d. Links display an l, and other special files—such as devices, sockets, and pipes—display c or b, s, and =, respectively.
+   - The next nine positions represent the nine permission switches. The first three switches apply to the file’s owner, the middle three to members of the file’s group, and the last three to “other” users. Each group of three switches contains a read switch, a write switch, and an execute switch, in that order. When a switch is on (permission granted), a letter appears: r for read, w for write, and x for execute. When a switch is off (permission denied), a dash (–) appears. In the case of readme.txt, above, you can see that the owner has permission to read and write, the group has permission to read and write, and others only have read permission. In the case of the above directory called stuff, all users have read and execute permission (which means that all users can cd into the directory). However, only the owner and group have write permission and will be allowed to create files in the stuff directory.

# The Effective User Id

Access to files and processes will depend on your current username and current group affiliations. I say “current” because during a session it is possible for you to assume the id of a different user (that is, if you know that user’s password).

To see a list of your effective user id and group affiliations, you can use the id tool. The id command prints information about your current username, current group, and