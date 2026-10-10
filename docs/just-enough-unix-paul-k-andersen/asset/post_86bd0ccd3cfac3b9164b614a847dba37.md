
### 6.11 Printing on Other Printers

If your computer system has more than one printer attached to it, the simple line printer command used in the previous section will send your files to the default printer. You can specify another printer with the `-P` or `-d` option. To do this, you first have to know the code for the printer you are to use; ask your instructor, consultant, or system administrator.

-   Enter the line printer command and specify the printer and the file to be printed. On Berkeley UNIX you would type the following command, making sure to insert the proper printer code in place of `code`:

    ```
    $ lpr -Pcode 1999 (RETURN)
    ```

    Note that there is a space before the `-P` and before the file name, but not between the `-P` and the printer code.

    On AT&T UNIX, you would type the following command, inserting the printer code in place of `code`:

    ```
    $ lp -dcode 1999 (RETURN)
    ```

    Here again, there is a space before `-d` and before the file name, but not between the `-d` and the printer code.

### 6.12 Removing Unneeded Files

When a file is no longer useful, you should remove it so that it won't take up valuable storage space. This is done with the `rm` ("remove") command, which takes the pathname of the file to be removed. Since you probably don't need two copies of the summer 1999 calendar, remove one of them.

1.  **Use the `ls` command to check the file name.** Since on many systems you cannot retrieve a file once it has been removed, it is a good idea to be sure of the file name:

    ```
    $ ls (RETURN)
    ```

    ```
    1999 august99 july99 june99 summer99 vacation99
    ```

2.  **Type `rm`, followed by the file's pathname.** To remove `vacation99`, type the command line

    ```
    $ rm vacation99 (RETURN)
    ```

3.  **Verify that the file is gone.** UNIX does not tell you that the file has been removed, so you will have to check this yourself using the `ls` command:

    ```
    $ ls (RETURN)
    ```

    ```
    1999 august99 july99 june99 summer99
    ```

### 6.13 Command Summary

Each command is typed in after the UNIX shell prompt, and each is terminated by a `RETURN`. Note that `file`, `file1`, and `file2` may be simple file names or path-names.

#### Making Calendars

-   `cal m year`: show a calendar for the mth month of year
-   `cal year`: show a calendar for year
-   `cal year > file`: redirect calendar for year into file
-   `cal year >> file`: append calendar for year to file

#### Listing and Viewing Files

-   `ls`: list files in working directory
-   `cat file`: show contents of file all at once
-   `more file`: show contents of file one screen at a time; press space-bar to continue or q to quit
-   `pg file`: Like `more`. Press `RETURN` to see next screen, q to quit

#### Printing Files

-   `lpr file`: send file to default line printer (BSD UNIX)
-   `lp file`: send file to default line printer (AT&T UNIX)
-   `lpr -Pcode file`: send file to printer designated by code (BSD)
-   `lp -Dcode file`: send file to printer designated by code (AT&T)

#### Copying, Renaming, and Removing Files

-   `cp file1 file2`: copy file1 into file2; retain both copies of the file
-   `mv file1 file2`: move (i.e., rename) file1 to file2; retain only file2
-   `rm file`: remove (i.e., delete) file

### 6.14 Exercises

1.  What are the rules for selecting UNIX file names?

2.  Because of the need to make certain adjustments to the calendar, the month of September 1752 was a very unusual one. What was different about it?

3.  The `echo` command takes a line that you type in and repeats it back on the screen. Thus if you type

    ```
    echo This is fun!(RETURN)
    ```

    The computer will respond with

    This is fun!

    Redirect this phrase into a file named `fun`.

4.  Using the commands `who`, `who am I`, and `date`, append to the `fun` file a list of the users currently logged onto the computer, your login, and the current date.

5.  A hidden file has a name that begins with a period ( . ). Use the `cal` utility and the redirection operator ( `>` ) to create a file named `.hidden`, then use `ls` to list your files. Do you see the `.hidden` file? Now try the `ls -a` command. Does `.hidden` appear? What other hidden file entries do you see?

6.  Many UNIX systems offer a utility named `file`, which classifies files according to their contents. The utility examines the file and tries to determine what kind of information it may contain. Some of the classifications used by `file` are

    | ascii text | c program text | commands |
    | :--- | :--- | :--- |
    | data | directory | empty |
    | English text | executable | |

    Try out the `file` command on the files and directories in your system. Does `file` always classify files correctly?

## 7 TUTORIAL: WORKING WITH DIRECTORIES

A directory is a file that contains other files and directories. In this chapter, you will see how to create directories, move files between directories, rename files, and delete directories you no longer need.

### 7.1 Your Directory Structure Thus Far

If you have carefully followed the examples in the text and worked through all of the end-of-chapter exercises, your file system should resemble the structure shown in Figure 7-1. At this point, your home directory contains no subdirectories. You are now ready to create new subdirectories inside your home directory.

Figure 7-1
Your file system after completing the previous chapter.

![img](img/52d592fcd97ba67dcb2b4a36fde4eb4c_83_0.png)

### 7.2 Creating a Subdirectory

It’s time to make a directory to hold the calendars you made in the previous chapter. For this we use the `mkdir` (“make directory”) command.

1.  Select an appropriate name for the new directory. The rules for naming directories are the same as for files. (However, in this book we will capitalize the names of any new directories we create to distinguish them from ordinary files.) A descriptive name for a directory to hold calendars would be `Cal`.
2.  Enter `mkdir` followed by the new directory name. Remember to capitalize the directory name:

    ```
    $ mkdir Cal (RETURN)
    ```

3.  Use the `ls` command to see that the new directory exists:

    ```
    $ ls (RETURN)
    ```

    The new directory name should appear, along with the names of the files you made before:

    ```
    1999 Cal august99 fun july99 june99 summer99
    ```

    (If you have been following the examples in the text, your file system should resemble Figure 7−2.)

    > Note that the directory name `Cal` differs from the `cal` command—remember, UNIX is case-sensitive.

![img](img/52d592fcd97ba67dcb2b4a36fde4eb4c_84_0.png)

### 7.3 Moving Files between Directories

> Recall that you used *mv* before to rename a file.

When a new subdirectory is first created, it contains no files. In this section, you will see how to move a file to a new subdirectory using the *mv* (“move”) command, which you previously used to rename files.

1.  **Type the *mv* command, the file's name, and the destination directory's name.** To put `1999` into the directory *Cal*, enter the command line

    ```
    $ mv 1999 Cal (RETURN)
    ```

    This puts `1999` inside *Cal* (see Figure 7-3).

2.  **List the files in your home directory.** Check to see that `1999` has indeed been moved:

    ```
    $ ls (RETURN)
    ```

    The `1999` file will not appear because it is now inside the *Cal* subdirectory:

    ```
    Cal august99 fun july99 june99 summer99
    ```

![img](img/52d592fcd97ba67dcb2b4a36fde4eb4c_85_0.png)

### 7.4 Creating Directories Using Pathnames

Your next task is to create a subdirectory inside `Cal` to hold monthly calendars. A good, descriptive name for this directory is `Months`. Since this is to go inside `Cal`, the pathname of the new directory relative to your home directory will be `Cal/Months`.

-   Enter the **`mkdir` command, followed by the *pathname of the new directory*. Thus, to create a directory `Months` inside the directory `Cal`, type

    ```
    $ mkdir Cal/Months (RETURN)
    ```

With the creation of `Months`, your directory structure should resemble the one shown in Figure 7-4.

![img](img/52d592fcd97ba67dcb2b4a36fde4eb4c_86_0.png)
