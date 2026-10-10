
## Editing and Navigating

Now that you know how to open a file using Vim, the next thing that you need to understand is how to modify a file using Vim. The first thing that you will notice when editing a vim file is that, if you use the arrow keys to move the cursor and start typing to edit the file, nothing happens. The reason is that you have to enter the Insert mode in Vim.

In order to enter the Insert mode in Vim, you simply type the letter “a.” Once you do that, you will be able to edit and start typing your modifications on the file. When you are done making your modifications to the file, what you do to get out of the Insert mode is hit the ESC key on your keyboard.

So the next thing is, if you edit a configuration file, especially like the php.ini or any other main configuration file, keep in mind that these are really long documents. If you are trying to edit a single word or value inside that extremely long file, finding that single word or value alone can be a tedious task.

In order to find something in Vim, there are two simple commands that you can use to make your life easy. First, make sure that you are out of the Insert mode. Once you are out of Insert mode, go ahead and type the command below:

```
:/ <name>
```

That is colon, followed by a forward slash, and then a space, and then word of value that you are looking for within the file that you are trying to modify. Again, remember that capitalization is crucial. Make sure you capitalize the name correctly, or else Linux will not able to find what you are looking for. And if it did find something, it will be the incorrect one.

What this command does is it looks from the place that you are at—your cursor— all the way down through the rest of the document. It will look for the word of value that you typed in your find command. Now, the important thing with searching is that you can put in wildcard characters.

Let us say you are looking for the word max within the configuration file. To look for max, you need to type in the find command below:

```
:/ max
```

Now, one of the things most Linux experts do is whenever they are looking for a specific string in a file, they put a wildcard character, specifically an asterisk symbol, before and after the name of the string. The command would then look like this:

```
:/ *max*
```

What the above command says is you are looking for anything that has max in the middle; whether it is a part of a string or a standalone string. Because sometimes if there is a space or there is a little character before or after the string, it may not show up when you do the find command. This is the purpose of the wildcard in cases like these.

Now take note that with the forward slash, $Vim$ will search from where your cursor is at going down. So, what if you have reached the end of the file and you did not find what you are looking for? At this point, your cursor is at the end of the file. In order to make a search upwards from where your cursor is at, simply type the command below:

```
:/? <name>
```

That is colon, followed by a forward slash, followed by a question mark, a space, and then the string or value that you are looking for. This is what will make the search go upwards from where your cursor is at.

Now, what if there are multiple instances of the string or value that you are looking for in a $vim$ file? Well, when you do a search, $Vim$ will automatically halt on the first instance of the string or value that you are looking for. To move to the next instance, you just need to hit the letter \"$n$\" on the keyboard. This is the equivalent of \"Find Next\" in the Windows operating system. As you can see, navigating in $Vim$ is really easy. The above commands are all it takes to open, navigate, search, and edit files in $Vim$.

## Exiting and Saving

The next thing we need to talk about is how open, exit, and save files within Vim. So far, what we discussed opening Vim files from the command prompt. So now, let us discuss how to open up other Vim files while inside Vim itself.

If you need to open a file and you are already in Vim—so you need to switch to another file—just type the command below:

```
`:e <filename>`
```

That is a colon, followed by a lowercase letter e, a space, and then the file name. Again, make sure you are out of Insert mode when you do this. If you are in Insert mode and you type in this command, what will happen is Vim will just type in the command within the file itself. It will not be interpreted as a command to open up a different file.

That is all you have to do to open up another Vim file from within Vim. Now, let us say you open up a file and you look around in them. But then, you decide that you do not want to change anything and you need to get out of that file. What you do in this instance is type in the command below:

```
`:q`
```

That is a colon, and then followed by the lowercase letter q. This command will exit you out of Vim. Of course, you have to press ENTER after typing in each command in order to execute them.

There will be times when you also have to force quit out of Vim. There may be times when Vim has become unresponsive or it does not want to accept the normal quit command. In cases like these, you want to force Vim to exit. To do that you have to put an exclamation mark after the lowercase letter q.

```
`:q!`
```

Whether Vim got stuck or has become unresponsive to other commands, putting an exclamation mark after the lowercase letter q will definitely get you out of the Vim application. Only use this command if nothing else works. Keep in mind that if you are quitting Vim normally using the :q or :q! command, no changes will be saved in the file that you are trying to edit—unless you saved the changes first before trying to execute the quit command.

Now, let us say Vim locked up for some reason and you have already entered numerous changes in the file. Of course, in order for you not to go through all the changes again, you want to save the file before quitting. In this instance, what you do is type in the command below:

```
`:wq`
```

That is a colon, followed by the lowercase letter w, and then followed by the lowercase letter q. The lowercase letter w stands for “write”, while the lowercase letter q stands for quit. So this will save whatever changes you made to the file first before quitting Vim.

The next thing is, let us say you made some changes to the file but you do not want it to be saved to the original file. So you are basically trying to do a “save as” command here. To do that, just type in the command below:

```
:w <new filename>
```

That is colon, followed by a lowercase letter w, a space, and then the name of the new file that you want to create and save into. This command will save the file that you edited to a new file. This is particularly useful when you do not want to overwrite the original file and you want to preserve it for some reason.

## Chapter 7: Advanced Linux Navigation

In this chapter, we will talk about advanced Linux navigation. In chapter 5, we have already talked about how to change directories in Linux. Now, we will discuss how to find folders in Linux, how you make and remove directories, how you copy files, and then finally how you mount drives in Linux.

### Changing Directories and Finding Files

In the last chapter, we talked about how you edit configuration files using *Vim*, which is pretty essential in Linux. Now, as you sit there and look at the file system, you probably have no idea where those configuration files are in the first place. If you wanted to edit the *php.ini* file for example, the question that you may be asking since you are a beginner in Linux is, where is the *php.ini* file located?

So, to find any particular file that you want to edit, you must first learn how to get to the folder or directory where that particular file is located. Again, to change directories, all you need to do is make use of the *cd* command just like in Windows. The syntax to change directory is:

```
$ cd <name of folder>
```

Now, there is more to this command than meets the eye. Remember, Linux is exceptionally literal when it comes to the interpretation of commands syntaxes. Again, let us make use of the diagram below:

![](img/38783e2b6fd4fbccebb177aa2953d843_77_0.png)

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
