```
$ cd /home/alex/literature
$ pwd
/home/alex/literature
$ cd
$ pwd
/home/alex
$ cd literature
$ pwd
/home/alex/literature
```

**Figure 6-9** cd changes your working directory

by Alex. When used without an argument, cd makes your home directory the working directory, as it was when you logged in. The second cd command in Figure 6-9 does not have an argument so it makes Alex's home directory the working directory. Finally, knowing that he is working in his home directory, Alex uses a simple file-name to make the literature directory his working directory (cd literature) and confirms the change with pwd.

# The working directory versus your home directory

**tip**

The working directory is not the same as your home directory. Your home directory remains the same for the duration of your session and usually from session to session. Immediately after you log in, you are always working in the same directory: your home directory.

Unlike your home directory, the working directory can change as often as you like. You have no set working directory, which explains why some people refer to it as the current directory. When you log in and until you change directories by using cd, your home directory is your working directory. If you were to change directories to Scott's home directory, then Scott's home directory would be your working directory.

# THE . AND .. DIRECTORY ENTRIES

The mkdir utility automatically puts two entries in each directory you create: a single period (.) and a double period (..). The . is synonymous with the pathname of the working directory and can be used in its place; the .. is synonymous with the pathname of the parent of the working directory. These entries are hidden because their filenames begin with a period.

With the literature directory as the working directory, the following example uses .. three times: first to list the contents of the parent directory (/home/alex), second to copy the memoA file to the parent directory, and third to list the contents of the parent directory again.

```
$ pwd
/home/alex/literature
$ ls ..
demo literature memoA names temp
$ cp memoA ..
$ ls ..
demo literature memoA names temp
```