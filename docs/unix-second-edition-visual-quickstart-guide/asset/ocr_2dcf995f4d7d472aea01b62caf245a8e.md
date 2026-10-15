# Understanding File Ownership and Permissions

Unix provides three levels of file ownership:

+   - **User.** Refers to the single userid that's primarily in charge of the file. You have this level of ownership for the files you create.

+   - **Group.** Refers to the group (of users) associated with a specific file. All users within a group have the same permissions for interacting with a file.

+   - **Other.** Refers to any users not identified with either the group or user for a file.

Within these groups, you can specify permissions for file access and rights in three categories:

+   - **Read.** Users with read permission can only view a file; they cannot make changes to it.

+   - **Write.** Users with write permission can make changes to or delete a file.

+   - **Execute.** Users with execute permission can run files (programs or scripts) and view directories.

In this chapter, we'll show you some of the commands that can be used (sometimes by you, usually by the root user) to set ownership and permissions. Keep in mind that you can set or change any permissions for files you create and possibly for files created by others; however, exactly which permissions and ownerships you can change depends on the system. Even if you don't currently need to change file ownerships or permissions, you should take a quick read through this chapter to see what options might be available to you.

# Tips

+   - An interesting twist on this whole ownership issue is that not all "owners" are people. Programs or processes (discussed in Chapter 9) run as a specific user, and if they create files, those files have permissions reflecting the individual and group membership of the program. See Chapter 9 for more information.

+   - Some Unix-like operating systems have additional or supplementary means of controlling access to specific files. Usually, though, you'll know if such a system is in use. For now, just know that such things exist: the procedures in this chapter will handle 99 percent of your needs.