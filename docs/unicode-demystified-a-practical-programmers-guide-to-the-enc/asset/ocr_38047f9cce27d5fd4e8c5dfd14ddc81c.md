![](bbox=[0.238, 0.045, 0.938, 0.312])

**Figure 4-6** Relative pathnames

working directory be referenced by short relative pathnames: two filenames separated by a slash. When you manipulate files in a large directory structure, short relative pathnames can save time and aggravation. If you choose a working directory that contains the files used most for a particular task, you need to use fewer long, cumbersome pathnames.

# # Home Directory

When you first log in on a GNU/Linux system, your working directory is your home directory. To display the absolute pathname of your home directory, you use pwd just after you log in (Figure 4-7).

Without any arguments, the utility displays a list of the files in the working directory. Because your home directory has been the only working directory you have used so far, it has always displayed a list of files in your home directory. (All the files you have created up now were created in your home directory:)

**cd**: Changes to Another Working Directory

The cd (change directory) utility makes another directory the working directory but does not change the contents of the working directory. The first cd command in Figure 4-8 makes the /home/alex/literature directory working directory, as verified by pwd.

```
login: alex
Password:
Last login: Wed Oct 20 11:14:21 from zach
$ pwd
/home/alex
```

**Figure 4-7** Log in