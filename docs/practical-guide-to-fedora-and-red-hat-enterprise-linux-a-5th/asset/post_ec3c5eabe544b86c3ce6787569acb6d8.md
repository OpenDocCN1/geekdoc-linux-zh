
Table 6-2 summarizes the utilities introduced in this chapter.

### Table 6-2: Utilities introduced in Chapter 6

| **Utility** | **Function** |
|---|---|
| cd | Associates you with another working directory (page 196) |
| chmod | Changes the access permissions on a file (page 204) |
| getfacl | Displays a file’s ACL (page 208) |
| ln | Makes a link to an existing file (page 214) |
| mkdir | Creates a directory (page 195) |
| pwd | Displays the pathname of the working directory (page 192) |
| rmdir | Deletes a directory (page 200) |
| setfacl | Modifies a file’s ACL (page 208) |

## EXERCISES

1.  Is each of the following an absolute pathname, a relative pathname, or a simple filename?
    - a. milk.co
    - b. correspond/business/milk.co
    - c. /home/alex
    - d. /home/alex/literature/promo
    - e. ..
    - f. letter.0610
2.  List the commands you can use to perform these operations:
    - a. Make your home directory the working directory
    - b. Identify the working directory
3.  If your working directory is /home/alex with a subdirectory named literature, give three sets of commands that you can use to create a subdirectory named classics under literature. Also give several sets of commands you can use to remove the classics directory and its contents.
4.  The df utility displays all mounted filesystems along with information about each. Use the df utility with the -h (human-readable) option to answer the following questions.
    - a. How many filesystems are mounted on your Linux system?
    - b. Which filesystem stores your home directory?
    - c. Assuming that your answer to exercise 4a is two or more, attempt to create a hard link to a file on another filesystem. What error message do you get? What happens when you attempt to create a symbolic link to the file instead?
5.  Suppose that you have a file that is linked to a file owned by another user. How can you ensure that changes to the file are no longer shared?
6.  You should have read permission for the /etc/passwd file. To answer the following questions, use cat or less to display /etc/passwd. Look at the fields of information in /etc/passwd for the users on your system.
    - a. Which character is used to separate fields in /etc/passwd?
    - b. How many fields are used to describe each user?
    - c. How many users are on your system?
    - d. How many different login shells are in use on your system? (Hint: Look at the last field.)
    - e. The second field of /etc/passwd stores user passwords in encoded form. If the password field contains an x, your system uses shadow passwords and stores the encoded passwords elsewhere. Does your system use shadow passwords?
7.  If /home/jenny/draft and /home/alex/letter are links to the same file and the following sequence of events occurs, what will be the date in the opening of the letter?
    - a. Alex gives the command vim letter.
    - b. Jenny gives the command vim draft.
    - c. Jenny changes the date in the opening of the letter to January 31, 2008, writes the file, and exits from vim.
    - d. Alex changes the date to February 1, 2008, writes the file, and exits from vim.
8.  Suppose that a user belongs to a group that has all permissions on a file named jobs_list, but the user, as the owner of the file, has no permissions. Describe which operations, if any, the user/owner can perform on jobs_list. Which command can the user/owner give that will grant the user/owner all permissions on the file?
9.  Does the root directory have any subdirectories that you cannot search as a regular user? Does the root directory have any subdirectories that you cannot read as a regular user? Explain.
10. Assume that you are given the directory structure shown in Figure 6-2 on page 189 and the following directory permissions:

    ```
    d--x---x---  3 jenny pubs 512 Mar 10 15:16 business
    drwxr-xr-x  2 jenny pubs 512 Mar 10 15:16 business/milk_co
    ```

    For each category of permissions—owner, group, and other—what happens when you run each of the following commands? Assume that the working directory is the parent of **correspond** and that the file **cheese_co** is readable by everyone.
    - a. cd **correspond**/business/milk_co
    - b. ls -l **correspond**/business
    - c. cat **correspond**/business/**cheese_co**

## ADVANCED EXERCISES

11. What is an inode? What happens to the inode when you move a file within a filesystem?
12. What does the .. entry in a directory point to? What does this entry point to in the root (/) directory?
13. How can you create a file named ~i? Which techniques do not work, and why do they not work? How can you remove the file named ~i?
14. Suppose that the working directory contains a single file named **andor**. What error message do you get when you run the following command line?

    ```
    $ mv **andor** and/or
    ```

    Under what circumstances is it possible to run the command without producing an error?
15. The ls -i command displays a filename preceded by the inode number of the file (page 215). Write a command to output inode/filename pairs for the files in the working directory, sorted by inode number. (*Hint:* Use a pipe.)
16. Do you think that the system administrator has access to a program that can decode user passwords? Why or why not? (See exercise 6.)
17. Is it possible to distinguish a file from a hard link to a file? That is, given a filename, can you tell whether it was created using an ln command? Explain.
18. Explain the error messages displayed in the following sequence of commands:

    ```
    $ ls -l
    total 1
    drwxwr-x-x 2 alex pubs 1024 Mar 2 17:57 dirtmp
    $ ls **dirtmp**
    $ rmdir **dirtmp**
    rmdir: **dirtmp**: Directory not empty
    $ rm **dirtmp**/*
    rm: No match.
    ```

# 7 THE SHELL

This chapter takes a close look at the shell and explains how to use some of its features. For example, it discusses command-line syntax and also describes how the shell processes a command line and initiates execution of a program. The chapter also explains how to redirect input to and output from a command, construct pipes and filters on the command line, and run a command in the background. The final section covers filename expansion and explains how you can use this feature in your everyday work.

The exact wording of the shell output differs from shell to shell: What your shell displays may differ slightly from what appears in this book. Refer to Chapter 9 for more information on **bash** and to Chapter 27 for information on writing and executing **bash** shell scripts.

223

- The Command Line . 224
- Standard Input and Standard Output . 230
- Redirection . 232
- Pipes . 238
- Running a Program in the Background . 241
- kill: Aborting a Background Job . 242
- Filename Generation/Pathname Expansion . 243
- Builtins . 247

## THE COMMAND LINE

The shell executes a program when you give it a command in response to its prompt. For example, when you give the `ls` command, the shell executes the utility program named `ls`. You can cause the shell to execute other types of programs—as shell scripts, application programs, and programs you have written—in the same way. The line that contains the command, including any arguments, is called the **command line**. In this book the term **command** refers to the characters you type on the command line as well as to the program that action invokes.

### SYNTAX

Command-line syntax dictates the ordering and separation of the elements on a command line. When you press the **RETURN** key after entering a command, the shell scans the command line for proper syntax. The syntax for a basic command line is

```
command [arg1] [arg2] ... [argn] RETURN
```

One or more **SPACES** must separate elements on the command line. The **command** is the name of the command, `arg1` through `argn` are arguments, and **RETURN** is the key-stroke that terminates all command lines. The brackets in the command-line syntax indicate that the arguments they enclose are optional. Not all commands require arguments: Some commands do not allow arguments; other commands allow a variable number of arguments; and others require a specific number of arguments. Options, a special kind of argument, are usually preceded by one or two hyphens (also called a dash or minus sign: `-`).

### COMMAND NAME

Some useful Linux command lines consist of only the name of the command without any arguments. For example, `ls` by itself lists the contents of the working directory. Most commands accept one or more arguments. Commands that require arguments typically give a short error message, called a **usage message**, when you use them without arguments, with incorrect arguments, or with the wrong number of arguments.

![](img/f28adb66a7398a382f0505e0ba74a872_264_0.png)

### ARGUMENTS

On the command line each sequence of nonblank characters is called a *token* or *word*. An **argument** is a token, such as a filename, string of text, number, or other object that a command acts on. For example, the argument to a **vim** or **emacs** command is the name of the file you want to edit.

The following command line shows `cp` copying the file named **temp** to **tempcopy**:

```
$ cp temp tempcopy
```
