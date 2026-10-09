This means that everyone belonging to the **course group**, and who *also* belongs to **authors or lecturers**, will be able to access the `material` directory. No other accounts will be able to access the directory.

Now, we can create the `book` directory as a subdirectory of the `material` directory. The `book` directory will be Read, Write, Execute accessible by the owner and the **authors group**. Other users will have only Read, Execute access. This is exactly what we want, because the `material` folder immediately above protects the `book` folder from unwanted access by students, so it is safe to leave Read and Execute access for others: in our case, others can *only* be the **lecturers group**. We must not forget to activate the **Set GID Bit** on the folder, in order to allow our writers to cooperate nicely. So, these are the permissions for the `book` directory:

```
drwxrwsr-x 2 eziocdm writers 4096 Jan 19 11:04 book
```

# When root Is Not Necessary

We've mentioned already that the protection offered by Linux when working as a normal user is a definite advantage. Certainly, working as root all the time is one of the worst habits that a novice Linux user can develop. For example, suppose you're working as the **root user**, and you're cleaning up some unwanted files in your home directory, so you want to execute the following command:

```
# rm -rf /home/eziocdm/tmp/redundant
```

Now, consider what happens if you accidentally insert a space character, like this:

```
# rm -rf /home /eziocdm/tmp/redundant
```

Please **don't** try this out for yourself! The extra space character is almost invisible, but it completely changes the meaning of the command. The first of these commands will attempt to delete only the directory `/home/eziocdm/tmp/redundant` and its contents. But the second command will attempt to seek out and destroy the contents of every home directory on the system!

If you're working as root, then there's no protection – root is allowed to delete these directories, and they'll be wiped out in an instant.

You can protect yourself from accidents like this by working as a normal user. Normal users are prevented from deleting such important directories, and this is what happens when you try:

```
$ rm -rf /home /eziocdm/rmp/redundant
rm: cannot remove '/home': Permission denied
```