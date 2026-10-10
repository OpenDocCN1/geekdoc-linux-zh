of the file, it'll show a number. This number represents the UID that owns this file. If a new user is created with the same UID as the old user, the same UID will show up as the owner, making it appear as if the new user owns the file. Because of this behavior, it is important that you make sure you remove all of the files owned by a user when removing that user's account.

# ## SUMMARY

This chapter documents the nature of users under Linux. Much of what you read here also applies to other variants of UNIX, which makes administering users in heterogeneous environments much easier with different UNIX's than NT/UNIX.

The most significant issues covered were these:

+   - Each user gets a unique UID
+   - Each group gets a unique GID
+   - The /etc/passwd file maps UIDs to usernames
+   - Linux handles encrypted passwords in multiple ways
+   - Linux includes tools that help you administer users
+   - Should you decide to write your own tools to manage the user databases, you'll now understand the format for doing so

These changes are pretty significant for an administrator coming from the Windows 95/98/NT environment and can be a little tricky at first. Not to worry though, the UNIX security model is quite straightforward, so you should quickly get comfortable with how it all works.

If the idea of getting to build your own tools to administer users appeals to you, definitely look into books on the Perl scripting language. It is remarkably well suited for manipulating tabular data (such as the /etc/passwd file). With its networking facilities and NT support, Linux even lets you build a cross-platform adduser tool that can not only create and setup UNIX accounts but NT accounts as well. With so many books on Perl out there, each with a slightly different angle and assuming a slightly different level of programming background, it's tough to make a single book recommendation. Take some time and page through a few books at your local bookstore.