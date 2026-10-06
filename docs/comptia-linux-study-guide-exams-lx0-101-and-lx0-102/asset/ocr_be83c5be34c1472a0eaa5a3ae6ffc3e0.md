# EXERCISE 4.1 (Continued)

+   7. User2, try to access the file by typing cat testfile. The file should appear on the screen.

+   8. User2, try to change the name of the file by typing mv testfile changedfile. The system won't produce any feedback, but if you type ls, you'll see that the file's name changed. Note that user2 doesn't own the file but can rename it because user2 can write to the directory in the file resides.

+   9. User2, try to change the mode of the file by typing chmod 0600 changedfile. The system should respond with an Operation not permitted error because the file's owner may change its permissions.

+   10. User2, try to delete the file by typing rm changedfile. Depending on your configuration, the system may not ask for verification, but it should permit the deletion. This is despite the fact that user2 doesn't own the file but can write to the directory in the file resides.

+   11. User1, repeat step 5 to re-create the test file.

+   12. As user1, give the file more restrictive permissions by typing chmod 0640. Typing ls -1 should reveal permissions of --rw-r----, meaning that the file's owner can read and write the file, members of the file's group can read, and others are given no access.

+   13. As user2, repeat steps 7–10. The cat operation should fail with a Permission denied error, but it should produce the same results as they did the first time around. (If the cat operation succeeded, either user2 belongs to the file's group or the file's mode is set incorrectly.)

+   14. Log out of user1 and user2 accounts.

+   15. As root, type rm -r /tmp/scratch to delete the scratch directory and its contents.

If you like, you can perform tests with file permission modes and other file-manipulation commands before step 14.

# Setting the Default Mode and Group

When a user creates a file, that file has default ownership and permissions. The default owner is, understandably, the user who created the file. The default group is the user's primary group. The default permissions are configurable. These are defined by the user mask (umask), which is set by the umask command. This command takes as input an octal value that represents the bits to be removed from 777 permissions for directories, or from 666 permissions for files, when a new file or directory is created. Table 4.8 summarizes the effect of several possible umask values.