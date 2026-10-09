
## Exercises 30-43

- 30. You use ______ to change to a different directory.
- 31. You use ______ to remove a directory.
- 32. The ______ command will let you rename a directory.
- 33. The ______ command tells you how much free space remains on a hard drive.
- 34. To find out what your current directory is, use the ______ command.
- 35. You use the ______ command to create a new directory.
- 36. To find out how much space is occupied by files in the current directory and its subdirectories, use the ______ command.
- 37. Use the ______ command to get a file list that shows the date the file was created or last revised.
- 38. The listing for the directory containing Sallie’s business contacts is /home/Sallie/contacts. contacts is a ______ .
- 39. Sallie’s home directory is ______ .
- 40. To switch to your home directory, use the command ______ .
- 41. Before you delete a directory using **rmdir**, you must be certain that it is ______ .
- 42. No matter where she is in the directory structure, Sallie can list the *files* in her home directory by using the command ______ .
- 43. Sallie’s *userid* is **Sallie**. To change to Sallie’s home directory, you will use the command ______ .

### Match the Term

Match the term in the left column with the best choice from the right column. Note that, while more than one choice may be possible in matching the columns, only one choice for each item in the left-hand column will permit the correct matching process for *all* items in the left-hand column.

Left Column:
- 1. cd
- 2. df
- 3. du
- 4. ls
- 5. ls -l
- 6. mkdir
- 7. rmdir
- 8. mv
- 9. pwd
- 10. home directory
- 11. /home/userid
- 12. change to home directory
- 13. ..
- 14. .
- 15. file mode
- 16. delete files first

Right Column:
- A. list files
- B. show current directory
- C. space used
- D. change directory
- E. rename directory
- F. remove directory
- G. create directory
- H. list files with mode, date, and other info
- I. free space
- J. parent directory
- K. shows file owner
- L. rmdir
- M. /home/userid
- N. $HOME
- O. current directory
- P. cd

### Terms to Remember

- **directory**: A unit in the computer's file system, analogous to a folder in a physical filing cabinet.
- **directory structure**: Same as file system.
- **file system**: The collection of directories and subdirectories in which information is stored in a computer.
- **hierarchical**: When used in the phrase “hierarchical file system,” refers to a top-down directory structure, with the root at the top and directories and subdirectories below.
- **$HOME**: A shortcut designation for your home directory.
- **home directory**: Part of your account. It is your own subdirectory, usually in the directory /home.
- **root**: In a hierarchical computer file system, this is the topmost level of the system.
- **subdirectory**: A directory that is below another directory—analogous, in a physical filing cabinet, to putting one folder inside another folder.

### Commands to Remember

| Command | Description |
| :--- | :--- |
| cd | change directory |
| df | disk free; free space remaining on a hard drive |
| du | disk usage; space used in current directory and all subdirectories |
| ls | list files |
| ls -l | list files showing file type, file mode, size of file and date of creation or revision |
| man | display pages from the system manual |
| mkdir | make directory; create a new directory |
| mv | rename a directory |
| pwd | print working directory; shows you which directory is the current directory |
| rmdir | remove a directory |

### Special Characters

- ..(double dot): parent directory
- .(single dot): current directory

### Linux Directories Summary

- Linux uses a hierarchical file structure: root at the top, subdirectories below.
- Standard directories in Linux include /bin, /etc, /dev, /home, /tmp, and /usr.
- When you log in, Linux places you directly in your home directory.
- Your home directory is where you will usually save your files.
- $HOME is another way to designate your home directory. $HOME stands for /home/username.
- ls lists files.
- ls -l lists the files and provides much additional information about the files.
- The file mode determines both who can access your files and what they can do with your files.
- pwd displays your working directory.
- **cd** is the change directory command.
- The double dot `..` represents the parent directory.
- The single dot `.` represents the working directory.
- **mv** is the command you use to rename a directory.
- **mkdir** is the command you use to create a directory.
- **rmdir** is the command you use to remove a directory.
- **df** reports how much of space on your disk is free. It gives this report in blocks. The number **df** returns represents the entire file system.
- **du** reports how much of your disk is already occupied with files. It gives this report in blocks. The number **du** returns represents the working directory and all its subdirectories.

### Linux Made Easy Assessment

- Now that you have completed the material in both the CBT course and this guide, you can evaluate your progress with the *Linux Made Easy Assessment* program. After you have completed the Assessment, return to this guide and continue your work with module 6, *Linux Files*.

# Linux Files

## Introduction

In the previous module of the CBT, you learned about managing the Linux file system—the information "container." In this module of the CBT, you will learn about managing the information itself—individual files.

What kinds of files does Linux recognize? How do we name them? Rename them? Copy them? Move them? Delete them? Print them? How can we "borrow" a file with a link? Is there a way to read a text file? Add to a text file? Join text files? Find files? Find text within files? Linux gives us many tools for managing files, and you will learn about them in this module.

### In This Module You Will Learn:

- About Linux file types.
- How long Linux filenames can be.
- What characters are permitted in Linux filenames.
- About the wildcards * and ?
- How to manage your files.
- Why some filenames begin with a dot.
- How to link files.
- How to join files.
- How to append material to existing files.
- How to find files.
- How to print a text file.
- How to be certain your files are saved to disk.

Now go to the **Linux Files** module in the **Linux Made Easy CBT**. When you have finished the material in the CBT, return to this guide. When you get back here, do the exercises in **Try It Live!**, and then complete the questions in the **Check Yourself** and **Match** sections.

## Try It Live!

1. In the previous section of this guide, you created the subdirectory *practice*. Now we will put it to use. In this exercise, you will create two subdirectories.
   - a. Log in to your Linux terminal.
   - b. Type `cd practice`
   - c. Press <Enter>
   - d. Type `mkdir dir1`
   - e. Press <Enter>
   - f. Type `mkdir dir2`
   - g. Press <Enter>

2. Now list your home directory to make certain that you have two new directories. Your screen should look similar to Figure 6-1.
   - a. Type `ls -l`
   - b. Press <Enter>

```bash
$ ls -l
drwxr-xr-x 1 david Thu Sep 3 11:29 dir1
drwxr-xr-x 1 david Thu Sep 3 11:29 dir2
$
```

**Figure 6-1** *ls -l* Directory Listing

3. Change to the directory *dir1*.
   - a. Type `cd dir1`
   - b. Press <Enter>

In the next module of the CBT course, *Linux Tools*, we cover yet another function of the `cat` command: When combined with *redirection*, `cat` can be used to create text files directly from your keyboard. We introduce this function of `cat` at this point, however, so that you can create the files you will need to complete the exercises in this *Try It Live!* section.

When you enter text or commands at your keyboard, whatever you have typed is *input*. Input normally becomes *output* of some sort. Linux expects to send the output from your keyboard, *standard input*, to your monitor screen, *standard output*. In simpler terms, the system expects to take what you type and send it to your screen. That's why keyboard and monitor are referred to as *standard input* and *standard output*, respectively.

There are times when you want to change where the output is heading—you want to *redirect* it. There are many ways for this redirection to occur. We're going to use it here in one of its simplest forms.

Before we begin to create these files for our later exercises, we will experiment a bit with one simple option we have in creating these files: when to use `<Enter>`.

4. Create the first temporary file.
   - a. Type `cat > tempfile1`
     Note that there is a space both before and after the redirection symbol, `>`.
   - b. Press `<Enter>`
   - c. Type: `This is tempfile1.`
   - d. Press `<Ctrl-D>`
     <Ctrl-D> tells the system, “My input is complete. Create the file.”

5. Now take a look at `tempfile1`.
   - a. Type `cat tempfile1`
   - b. Press `<Enter>`
     Your screen will look similar to Figure 6-2.

```bash
$ cat tempfile1
This is tempfile1.
```

**Figure 6-2** Shell Prompt Next to Text of *tempfile1*
