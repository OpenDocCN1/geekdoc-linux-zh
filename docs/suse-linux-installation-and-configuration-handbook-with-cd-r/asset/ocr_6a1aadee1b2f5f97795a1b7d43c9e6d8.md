Or, if you are changing to a directory that is a child of the current directory, you could just type

```
$ cd doc
```

The shell then would assume that doc is a directory inside the one in which you are currently. To change the directory to the parent directory, you would type this command:

```
$ cd ..
```

In the previous command, the two dots (..) point to the parent directory of the directory in which you are currently. So, if you are in /home/john/doc and you run the previous command, you would end up in /home/john again. Type the command again and you would move to /home and so on.

To create a new directory, you use the mkdir command, which stands for Make Directory. For example, to create a directory called files in /home/john, you could type

```
$ mkdir /home/john/files
```

Again, if you are currently in /home/john, you could just type the following command:

```
$ mkdir files
```

The previous command causes the shell to assume you want to create this directory right here. If you want to create a whole family of directories in one step, you can use the -p option. For example, if you want to create the directory /home/john/files/pics, the command

```
$ mkdir -p /home/john/files/pics
```

creates the directory pics and all its parent directories if they don't already exist. This is easier than first creating /home/john/files and then creating /home/john/files/pics.

To remove a directory, you can use the rmdir command, which stands for Remove Directory. For example, to remove the directory called pics, you could type the following:

```
$ rmdir /home/john/files/pics
```

The directory must be empty, though. So, you should use the rm command to delete all the files in it first:

```
$ rm -r /home/john/files/pics
```