![](bbox=[0.16, 0.09, 0.67, 0.32])

# **FIGURE 2.13**
The $PATH$ variable.

There are three ways to get around this:

+   You can provide the full path to the executable file. For example, if you wanted to run an executable named **helloworld** located in `​/usr/myfiles`, you could enter `​/usr/myfiles/helloworld` at the shell prompt.

+   You can switch to the directory where the executable file resides. Then prepend `./` to the command. In the previous example, I would switch to the `​/usr/myfiles` directory and then enter `./helloworld` at the shell prompt. The `./` characters refer to the current directory. By prepending them to a command, you tell the shell program to look for the file in the command in the current directory.

+   You can add `./` to the *PATH* variable. This will direct the command interpreter to check the local directory regardless of the current directory.

Another issue you need to be aware of is one we briefly discussed earlier in this chapter. Linux file names and directory names are case sensitive. Hence, Linux commands are also case sensitive. If the executable file you are going to run is **HelloWorld**, you must use **HelloWorld** at the command prompt. **HelloWorld**, **HELLOWORLD**, or **helloWorld** won't work. Linux sees each of these as different files.

This applies to directory names as well. If you're calling `​/usr/myfiles​/helloWorld`, you must enter the command using the exact case. `​/Usr/MyFiles/helloworld` will point the command interpreter to a completely different directory structure.

A final issue to be aware if is the fact that each user has his or her own *PATH* variable. If you log in as root, you will have directories in your *PATH* variable that won't exist if you log in as a different user.