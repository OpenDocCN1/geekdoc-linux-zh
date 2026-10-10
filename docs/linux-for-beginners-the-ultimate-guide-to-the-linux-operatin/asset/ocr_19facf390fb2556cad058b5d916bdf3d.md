# Changing Directories and Finding Files

In the last chapter, we talked about how you edit configuration files using *Vim*, which is pretty essential in Linux. Now, as you sit there and look at the file system, you probably have no idea where those configuration files are in the first place. If you wanted to edit the *php.ini* file for example, the question that you may be asking since you are a beginner in Linux is, where is the *php.ini* file located?

So, to find any particular file that you want to edit, you must first learn how to get to the folder or directory where that particular file is located. Again, to change directories, all you need to do is make use of the *cd* command just like in Windows. The syntax to change directory is:

```
$ cd <name of folder>
```

Now, there is more to this command than meets the eye. Remember, Linux is exceptionally literal when it comes to the interpretation of commands syntaxes. Again, let us make use of the diagram below:

![](bbox=[0.2, 0.38, 0.81, 0.63])

If for example you are in the *var* directory/folder and you want to go to the *abc* folder, all you need to do is type:

```
$ cd abc
```

Now, if for example you are in the *var* folder and you want to go to the *etc* folder, just typing in `$ cd etc` from within *var* will not work. Because then Linux will think that you want to go to the *etc* folder that is within the *var* folder, which does not exist.

What you must do is type the command below:

```
$ cd /etc
```

Take note of the forward slash before the name of the directory that you want to go to. This forward slash will tell Linux to first go to the *root* directory and then find the *etc* folder or directory. Now, Linux will now be able to successfully bring you to the *etc* folder since it is able to locate it in the *root* directory.