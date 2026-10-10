The Don sees that his two print jobs are first in line. Both are small, so they should be done soon.

# Example 5.12 Canceling Print Jobs with lprm

At the last second, Don Quixote decides to add to his weekly report. So, he cancels the printing of *mon_rep* for the time being:

```
$ lprm 302<Enter>
```

# cat Can Print, Too

Before we leave this topic and this chapter, it is worth pointing out that the cat command can also be used to print text and files. To use cat in this manner also requires redirection, which we have mentioned previously under *Viewing File Contents*.

# Exercises

+   1. Change to the /home/mydirectory/mydir directory. Use the touch command to create two zero-length files called myfile1 and myfile2 in your mydir directory:

```
$ cd mydir<Enter>
$ touch myfile1<Enter>
$ touch myfile2<Enter>
```

+   2. Display a long listing of the contents of your mydir directory. What are the sizes of myfile1 and myfile2?

```
$ ls -l<Enter>
```

+   3. View the long listing again, but this time display the inode numbers, too. What are the inode numbers of each file?

```
$ ls -li<Enter>
```

+   4. Using the pwd command, verify that you are in the home directory, /home/directoryname.