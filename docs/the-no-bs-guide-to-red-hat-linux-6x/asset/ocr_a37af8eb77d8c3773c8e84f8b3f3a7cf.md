# DELETING FILES

Ready to do a little damage? The rm command removes a file (assuming you have permission to do so) without even saying hasta la vista. Be sure you really want to delete your files before you use rm, because once the files are gone, they're not coming back. For example,

```
rm wallet
```

immediately deletes the file named wallet in the current directory without prompting. If you want to be prompted before the deletion, use the -i flag.

> NOTE: There is one little safety feature in rm—it won’t delete a directory (unless you use the -r flag).

One other rm flag is -f, which translates roughly to “Don’t ask me any questions—just delete the files.” While rm normally asks for confirmation before deleting a write-protected file, the -f (force) flag overrides this prompt.

Be careful with the rm command, since the multiuser nature of Linux does not allow for undelete as in DOS. As soon as you let go of the space occupied by a file, the operating system is likely to use it for something else.

# CREATING DIRECTORIES

If you have a bunch of related files scattered in your home directory, why not create a directory for them? Use the mkdir command as follows:

```
mkdir cooking
```

This creates a new directory named cooking in the current directory, into which you can move all those recipes for easy retrieval.