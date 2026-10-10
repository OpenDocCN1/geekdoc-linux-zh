# **Making, Deleting, Moving, Copying, Renaming**

Now we need to talk about making, deleting, moving, copying, and renaming files and folders in Linux. The first thing that we are going to do is talk about creating a folder. It is pretty straightforward. All you do is type:

```
$ sudo mkdir <name of directory/folder>
```

That is sudo, followed by a space, and then the mkdir parameter, another space, and then the name of the folder or directory that you want to make. As you can probably already guess, *mkdir* stands for “make directory.”

Keep in mind that if you do not put the full path of the directory, this command will simply create that directory or folder inside the directory that you are currently in.

![](bbox=[0.18, 0.33, 0.75, 0.54])

For example, let us say you are in the var directory and you want to create a *Notes* folder inside the *etc* directory. If you type:

```
$ sudo mkdir Notes
```

This command will just create the *Notes* folder in the *var* directory. To create the *Notes* folder in the *etc* directory from within *var*, you must type in the full path just like the one below:

```
$ sudo mkdir /etc/Notes
```

This way, Linux will go to the root directory first, and then into the etc directory, and within the etc directory create a Notes folder. Typing in the full file path will ensure that no matter where you are in the file system, you would be able to create the folder in the right location. That is all you need to do to create a folder or directory in Linux.

Deleting files or folders is just as simple. What you do is type the command below:

```
$ sudo rm <file or folder name>
```

That is sudo, a space, followed by the letters rm, another space, and then finally the name of the file or folder that you want to delete. As you may have already guessed, rm stands for remove. Let us say for example you want to delete a file named Notes. All you need to do is type: