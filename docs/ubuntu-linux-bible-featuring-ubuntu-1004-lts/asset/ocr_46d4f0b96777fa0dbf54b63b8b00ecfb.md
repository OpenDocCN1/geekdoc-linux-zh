# # Chapter 11: Using Command-Line Tools

In this section, I'll focus on the second approach because many of us may be a bit rusty in octal, and the symbolic mode is easier to visualize and use. I'll use the example file hello.sh, which happens to be a bash command file (shell script) that simply prints the string "Hello, World! in the shell window from which it is executed. Let's look at its default permissions:

```
$ ls -l hello.sh
-rw-r--r-- 1 vwh mwh 36 2006.03-18 16:30 hello.sh
```

As explained in detail in Chapter 4, the characters at the left portion of the ls command's long output describe the current file permissions. These permissions fall into four groups: the leading dash identifies the type of object that this is (a dash means it's a regular file), and the remaining three groups of three characters indicate the permissions of the owner of the file (vwh), the groups associated with that file (also named vwh), and the rights that all other users have to file. Each of these groups of three characters can have the following values (in order):

+   - r: The file or directory can be read.
- w: The file or directory can be written.
- x: The file can be executed or the directory can be searched for other files or directories.
- - The permission is not granted.

The two instances of vwh in the ls output, from left to right, identify the owner of the file and the group that is associated with it. In the sample output, we therefore can see that if the owner of the file can both read and write to the file, but that other members of the group vwh can only read the file, and all other users on the system can only read the file.

Because this is a shell script, I presumably want to be able to execute it. To make the file executable by its owner (me), I would issue the following command:

```
$ chmod u+x hello.sh
```

Listing the file again, we can see that the file is now marked as being executable by its owner:

```
$ chmod u+x hello.sh
$ ls -al hello.sh
-rwxr-xr-x 1 vwh users 36 2006.03-18 16:30 hello.sh
```

If I want others in the group and all other users on the system to be able to execute this shell script, I could issue the following commands to make those changes and verify them:

```
$ chmod g+x hello.sh
$ ls -al hello.sh
-rwxr-xr-x 1 vwh users 36 2006.03-18 16:30 hello.sh
$ chmod a+x hello.sh
$ ls -al hello.sh
-rwxrwxr-xr-x 1 vwh users 36 2006.03-18 16:30 hello.sh
```