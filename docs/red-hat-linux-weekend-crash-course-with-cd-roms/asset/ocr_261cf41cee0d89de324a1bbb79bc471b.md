Many users use the alias feature to give more familiar names to common commands. If you are a DOS user and you use the md command to create a directory, you can simply define md as an alias for mkdir (the Linux command that creates a new directory). You do this as follows:

```
alias md=mkdir
```

Now, you can type md dirname to create a new directory named dirname. Another good use of an alias is to redefine a dangerous command, such as rm, to make it safer. By default, the rm command deletes one or more specified files. If you type rm * by mistake, rm deletes all files in your current directory. I learned this the hard way one day when I wanted to delete all files that ended with .xwd. (These files contained old screen images that I no longer needed.) I intended to type rm *.xwd, but somehow I ended up typing rm * .xwd. I got the following message:

```
rm: .xwd: No such file or directory
```

At first I was puzzled by the message, so I typed ls to see the directory's contents again. When the listing showed nothing, I realized that I had an extra space between the * and .xwd. All the files in that directory, of course, were gone forever.

The rm command provides the -i option, which asks for confirmation before deleting a file. To make that option a default, add the following alias definition to the .bash_profile file in your home directory:

```
alias rm='rm -i'
```

From now on, when you use rm to delete a file, the command first asks for confirmation as follows:

```
rm .bash_profile
rm: remove `.bash_profile'? n
```

Press y to delete the file; otherwise, press n.

# Running commands in the background

When you use MS-DOS, you have no choice but to wait for each command to complete before you enter the next command. (You can type ahead a bit, but the MS-DOS system can hold only a few characters in its internal buffer.) Linux,