
# Chapter 1. A Quick Review of the Basics

Another notational convention is the single period ., which always refers to the current directory. That'll become important later in the book when you want to specify a shell script in the current directory, not one in the PATH. We'll explain this in more detail soon.

## Displaying Your Working Directory: The pwd Command

The pwd command helps you to "get your bearings" by telling you the name of your current working directory.

Recall the directory structure from Figure 1.3. The directory that you are placed in when you log into the system is your home directory. You can assume from Figure 1.3 that the home directory for the user steve is /users/steve. Therefore, whenever steve logs into the system, it will automatically be placed inside this directory. To verify that this is the case, the pwd (print working directory) command can be executed:

```
$ pwd
/users/steve
$
```

The output from the command verifies that steve's current working directory is /users/steve.

## Changing Directories: The cd Command

You can change your current working directory by using the cd command. This command takes as its argument the name of the target or destination directory.

Let's assume that you just logged into the system and were placed in your home directory, /users/steve. This is depicted by the arrow in Figure 1.4.

You know that two directories are "below" steve's home directory: documents and programs. This can be easily verified at the terminal by issuing the ls command:

```
$ ls
documents
programs
$
```

The ls command lists the two directories documents and programs the same way it listed other ordinary files in previous examples.

![](img/dc544c8aef1333b25eff1c794c2e5ec2_32_0.png)

Figure 1.4 Current working directory is steve

To change your current working directory, issue the cd command, followed by the name of the new directory:

```
$ cd documents
$ 
```

After executing this command, you will be placed inside the documents directory, as depicted in Figure 1.5.

![](img/dc544c8aef1333b25eff1c794c2e5ec2_32_1.png)

Figure 1.5 cd documents

You can verify at the terminal that the working directory has been changed by using the pwd command:

```
$ pwd
/users/steve/documents
$
```

The easiest way to move up one level in a directory is to reference the .. shortcut with the command

```
cd ..
```

because by convention .. always refers to the directory one level up (see Figure 1.6).

```
$ pwd
/users/steve
$
```

![](img/dc544c8aef1333b25eff1c794c2e5ec2_33_0.png)

Figure 1.6 cd ..

If you wanted to change to the letters directory, you could get there with a single cd command by specifying the relative path documents/letters (see Figure 1.7):

```
$ cd documents/letters
$ pwd
/users/steve/documents/letters
$
```

## Working with Directories

![](img/dc544c8aef1333b25eff1c794c2e5ec2_34_0.png)

Figure 1.7 documents/letters

You can get up to your home directory by using a single `cd` command to go up directories as shown:

```
$ cd ../
$ pwd
/users/steve
$ 
```

Or you can get back to the home directory by a full pathname rather than a relative one:

```
$ cd /users/steve
$ pwd
/users/steve
$ 
```

Finally, there is a third way to get back to the home directory that is also the easiest. Typing the command `cd` without an argument always moves you back to your home directory, no matter where you are in the file system:

```
$ cd
$ pwd
/users/steve
$ 
```

## More on the ls Command

When you type the `ls` command, the files in the current working directory are listed. You can also use `ls` to obtain a list of files in other directories by supplying an argument to the command. First, get back to your home directory:

```
$ cd
$ pwd
/users/steve
$ 
```

Let's take a look at the files in the current working directory:

```
$ ls
documents
programs
$
```

If you supply the name of one of these directories to the `ls` command, you can get a list of the contents of that directory. So you can find out what's contained in the documents directory by typing the command `ls documents`:

```
$ ls documents
letters
memos
proposals
$
```

To take a look at a subdirectory memos, you can follow a similar procedure:

```
$ ls documents/memos
dact
plan
$
```

If you specify a nondirectory file argument to the `ls` command, you simply get that filename echoed back at the terminal:

```
$ ls documents/memos/plan
documents/memos/plan
$
```

Confused? There's an option to the `ls` command that lets you determine whether a particular file is a directory, among other things. The `-l` option (the letter l) provides a more detailed description of the files in a directory. If you were currently in steve's home directory, here's what the `-l` option to the `ls` command produces: 

```
$ ls -l
total 2
drwxr-xr-x 5 steve DP3725 80 Jun 25 13:27 documents
drwxr-xr-x 2 steve DP3725 96 Jun 25 13:31 programs
$
```

The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory

Confused? There's an option to the `ls` command that lets you determine whether a particular file is a directory, among other things. The `-l` option (the letter l) provides a more detailed description of the files in a directory. If you were currently in steve's home directory, here's what the `-l` option to the `ls` command produces: 

```
$ ls -l
total 2
drwxr-xr-x 5 steve DP3725 80 Jun 25 13:27 documents
drwxr-xr-x 2 steve DP3725 96 Jun 25 13:31 programs
$
```

The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

The next characters on the line define the permissions of that particular file or directory. These access modes apply to the file, owner, group, and others. The next columns show the number of hard links to the file, followed by the owner, the group, the size of the file in bytes, the time of the last modification, and the filename. The first line of the display is the count of blocks (1,024 bytes) of storage that the listed files use. Each successive line displayed by the `ls -l` command contains information about a file in the directory. The first character on each line indicates what type of file it is: `d` for a directory, `-` for a file, `b`, `c`, `l`, or `p` for a special file.

## Creating a Directory: The mkdir Command

Use mkdir to create directories. The argument to this command is simply the name of the directory you want to create. For example, assume that you are still working with the directory in Figure 1.7 and that you want to create a new directory called misc at the same level as the documents and programs. If you were currently in your home directory, typing the command mkdir would achieve the desired effect:

```
$ mkdir misc
$ 
```

If you run ls, you will have the new directory listed:

```
$ ls
documents
misc
programs
$
```

The directory structure now appears as shown in Figure 1.8.

![](img/dc544c8aef1333b25eff1c794c2e5ec2_37_0.png)

Figure 1.8 Directory structure with newly created misc

## Copying a File from One Directory to Another

The cp command can be used to copy a file from one directory into another. For example, you can copy the file wb from the programs directory into a file called wbx in the misc directory as:

```
$ cp programs/wb misc/wbx
```

Because the two files are in different directories, they can safely have the exact same name:

```
$ cp programs/wb misc wb
```

When the destination file is going to have the same name as the source file (in a different directory, of course), it is necessary to specify only the destination directory as the second argument:

```
$ cp programs/wb misc
```

When this command gets, the Unix system recognizes the second argument as a directory and copies the source file into that directory. The new file is given the same name as the source file.

You can copy more than one file into a directory by listing the files to be copied prior to the name of the destination directory. If you were currently in the programs directory, the command

```
$ cp wb collect mon ..//misc
```

would copy the three files wb, collect, and mon into the misc directory, with the same filenames.
