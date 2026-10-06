
## Pathnames

In the following example /home/alex is the working directory. The example uses a relative pathname to copy the file letter to the /home/alex/literature/promo directory. The copy of the file has the same filename letter.0610:

```
$ pwd
/home/alex
$ cp letter literature/promo/letter.0610
```

Use a text editor to create a file named letter if you want to experiment with the examples that follow.

Assuming Alex has not changed to another directory, the following command allows him to edit the copy of the file he just made:

```
$ vi literature/promo/letter.0610
.
```

If Alex does not want to use a long pathname to specify the file, he can use cd to make the promo directory the working directory before using vi.

```
$ cd literature/promo
$ pwd
/home/alex/literature/promo
$ vi letter.0610
.
```

If Alex wants to make the parent of the working directory (named /home/alex/literature) the new working directory, he can give the following command, which takes advantage of the .. directory entry:

```
$ cd ..
$pwd
/home/alex/literature
```

## Optional

## Special Pathnames

To save typing, the shells and some utilities, such as vi, recognize a few shortcuts in pathnames. The shell expands the characters ~/ (a tilde followed by a slash) at the start of a pathname into the pathname of your home directory. Using this shortcut, you can examine your .login file with the following command no matter which directory is your working directory:

```
$ less ~/.login
```

## Working with Directories

A tilde quickly references paths that start with you or someone's home directory. The shell expands tilde followed by a login name at the beginning of a pathname to the pathname of that user's home directory. Assuming he has permission to do so, Alex can examine Scott's login file with

```
$ less ~scott/.login
```

Refer to ~ "Tilde Expansion" on page 609 for a discussion of this topic.

## mv, cp: Moves or Copies a File

Chapter 3 describes the use of mv to rename files. However, mv is more general than that: You can use mv to move files from one directory to another (change the pathname of a file) and to change a simple filename.

When used to move one or more files to a new directory, the syntax of the mv command is

```
mv existing-file-list directory
```

If the working directory is /home/alex, Alex can use the following command to move the files names and temp from the working directory to the literature directory:

```
$ mv names temp
```

This command changes the absolute pathnames of the names and temp from /home/alex/names and /home/alex/temp to /home/alex/literature/temp. As most GNU/Linux commands, mv accepts either absolute or relative pathnames.![](aa8214d91cf502c43284529fb3b166_0.png) Figure 4-11 Directories and ordinary files

## Chapter 4 The GNU/Linux Filesystem

As you work with GNU/Linux and create more files, you will need to create directories, using mkdir, to keep the files organized. The mv utility is a useful tool for moving files from one directory to another. The cp utility works the same way that mv does but makes copies of the existing-file-list in the specified directory.

## mv: Moves a Directory

As it moves ordinary files from one directory to another, mv can also move directories. The syntax is similar except that you specify one or more directories, not ordinary files, to move:

```
mv existing-directory new-directory
```

If new-directory does not exist, the existing-directory must contain just one directory name, which mv renames the directory. Although directories can be renamed using mv, their contents cannot be copied unless you use the -r option (page 12). Refer to tar in Part III for other ways to copy.

## Access Permissions

Three types of users can access a file: the owner of the file (owner), a member of a group to which the owner belongs (group); and everyone else (other). A user can attempt to access an ordinary file in three ways: by trying to read from, write to, or execute it. Three types of users, each able to access a file in three ways, equal a total of nine possible ways to access an ordinary file.

## ls -l: Displays Permissions

When you call ls with the -l option and the name of an ordinary file, ls displays a line of information about the file. The file letter.0610 contains the text of a letter, and check_spell contains a shell script, written in a high-level programming language:

```
$ ls -l letter.0610 check_spell
-rw-r--r-- 1 alex 3355 May 2 10:52 letter.0610
-rwxr-xr-x 2 alex 852 May 5 14:03 check_spell
```

## 4-12 The columns displayed by ls -l

From left to right, the lines contain the following information (refer also to Figure 4-12):

- The type of file (first character)
- The file's access permissions (the next nine characters)
- The number of links to the file (see page 23)
- The name of the owner of the file (usually the person who created the file)
- The name of the group that has access to the file
- The size of the file in characters (bytes)
- The date and time the file was created or last modified
- The name of the file

The type of file (first column) for letter.0610 is a hyphen (-) because it is a regular file (directory files have a d in this column). The next three characters represent the access permissions for the owner of the file: r indicates read permission and w indicates write permission. The - indicates that the owner does not have execute permission; otherwise one would see x. In a similar manner the next three characters represent permissions for the group, and for other (everyone else). In the preceding example the owner of the file letter.0610 can read and write to it, whereas group and others can only read from the file, and no one is allowed to execute it. Although execute permission can be allowed for any file, it does not make sense to assign execute permission to a file that contains a document, such as a letter. The check_spell file is an executable shell script, and execute permission is appropriate (The owner, group, and others have execute access permission.)

## chmod: Changes Access Permissions

The owner of a file controls which users have permission to access the file and how they can access it. When you own a file, you can use the chmod (change mode) utility to change access permissions for that file. In the following example chmod adds (+) read and write permission (rw) for all (a) users:

## You Must Have Read Permission to Execute a Shell Script

Because a shell needs to read a shell script (an ASCII file containing commands) before it can execute the commands within the script, you must have read permission to the shell file containing the script in order to execute it. You also need execute permission to execute a script directly on the command line. Binary (program) files do not need to be read; they are executed directly. You need only execute permission to run a binary (nonshell) program.

```
$ chmod a+rw letter.0610
$ ls -l letter.0610
-rw-rw-rw-- 1 alex 3355 May 2 10:52 letter.0610
```

In the next example chmod removes (--) and execute (rx) permissions for users other (o) than the owner of the file (Alex) and members of the group associated with the file (pubs):

```
$ chmod o-rx check_spell
$ ls -l check_spell
-rwxr-x-- 2 alex 852 May 5 14:03 check_spell
```

In addition to a (all) and o (for other), you can use g (for group) and u (for user), although user refers to the owner of the file, who or may not be the user of the file at any time in the argument to chmod. Refer to pages 545 and 1103 for more information on chmod.
