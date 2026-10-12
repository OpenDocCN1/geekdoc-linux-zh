# Deleting user accounts with userdel

The userdel command takes a single argument, which is the login name of the account to delete. If you supply the optional -r option, it also deletes the user's home directory and all the files in it. To delete the user account with login name mary, you would type this:

```
# userdel mary
```

To wipe out her home directory along with her account, type this:

```
# userdel -r mary
```

Files owned by the deleted user but not located in the user's home directory will not be deleted. The system administrator must search for and delete those files manually. The find command comes in very handy for this type of thing. I won't describe all the capabilities of the find command (that would take a very fat chapter of its own). I do, however, provide a few simple examples of how to use find to locate files belonging to a particular user, even when those files are scattered throughout a file system. You can even use the find command to delete or change the ownership of files, as they are located. Table 11-4 has a few examples of the find command in action.

# Table 11-4: Using find to Locate and Change User Files

| Find Command | Description |
|---|---|
| `find / -user mary` | Search the entire file hierarchy (start at /) for all files and directories owned by mary and print the filenames to the screen. |
| `find /home -user mary -exec rm -i {} \;` | Search for all files and subdirectories under /home owned by mary. Run the rm command interactively to delete each file. |
| `find / -user mary -exec chown jenny {} \;` | Search for all files and subdirectories under /home that are owned by user mary and run the chown command to change each file so that it is owned by jenny instead. |
| `find / -uid 500 -exec chown jenny {} \;` | This command is basically the same as the previous example, but it uses the user ID number instead of the user name to identify the matching files. This is useful if you have deleted a user before converting her files. |