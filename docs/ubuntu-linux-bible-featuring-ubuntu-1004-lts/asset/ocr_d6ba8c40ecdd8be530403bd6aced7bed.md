# Chapter 11: Using Command-Line Tools

# Moving Around in the Linux Filesystem

Just as you do when you use a graphical user interface, you will want to organize your files and directories in some logical fashion if you're working from the command line. Once you've organized things that way, you'll need to use the cd ("change directory") command, which does exactly what you'd expect. In hard-core Linux terms, the cd command changes your working directory to be the directory that you supply as an argument. For example, to change your directory into a directory named test, you'd simply execute the following command:

```
$ cd test
```

Tip
If you're hanging around hard-core Linux folks and want to fit in, refer to changing to another directory as cd'ing here. ■

If you don't know the name of the directory where you are currently working, that's somewhat scary, unless you use the pwd (process working directory) to provide that information. The pwd command lists the full pathname of the directory in which the current process (in this case, your shell) is running, as in the following example:

```
$ pwd
/home/wvh/test
```

You can change to any directory on your Linux system by specifying its full pathname as the argument to the cd command, as in the following example:

```
$ cd /usr/local
$ pwd
/usr/local
```

As you can see, my shell is now working in the /usr/local directory, and any other commands that I execute will be performed in that directory. For a convenience, if you execute the cd command without any arguments, the cd command automatically changes directory to your home directory, which is probably where most of your files and directories are located in the first place. You can also execute the cd - command to take you to the previous directory that you were working from.

As you work at the command line, you may find that you want to change to some other directory, one or two things, and then return to the directory that you started in. When changing directories frequently, it's handy to keep track of things like "Where did I come from?" To save time and mental energy, the bash shell provides built-in commands pushd and popd to track this you. The pushd command changes to a specified directory but remembers where you came from pushing the name of the directory to a list of previous locations known. Once you're done there, you can use the popd command to return to the directory that you came from, which removes it from the stack. If you're unfamiliar with the idea of a stack, the example of a stack is the spring-loaded stack of plates that you find at a cafeteria or your favorite lunch buffet. Pushing onto the stack is analogous to putting a new plate on the top of the stack of available plates. Popping off the stack is analogous to removing the top plate from the stack, which makes the next one available. ■