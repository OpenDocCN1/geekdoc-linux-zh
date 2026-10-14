
remove the file by typing rm expfile.txt followed by a tap on the ol’ ENTER key. The file will then be gone, and gone for good.

Now, double your pleasure by getting rid of the version of expfile.txt that is located in the subfolder sub. In this case, you need to specify where the file is because it isn’t in the folder that the Terminal is in. Just type rm command_exp/sub/expfile.txt, and then press ENTER. Oooh, very cool. Brings ya back, doesn’t it?

## $ rmdir

You will now continue the fun with the rmdir (remove directory) command, which is a bigger and more powerful version of the rm command.

You should use the rmdir command, like the rm command, with caution. There are no do-overs with rmdir. Once you remove a directory or folder with this command, it is gone for good.

To try this command, you can get rid of that sub folder you created. Type rmdir command_exp/sub, and press ENTER. The sub folder should now be gone.

Finally, to round out the fun, use the rmdir command once more to get rid of the command_exp folder you created earlier. You’ve probably got it down by now, but just in case you don’t, type rmdir command_exp, and then press ENTER.

## $ chmod

In Chapter 7, you learned how to change file permissions via the Nautilus interface. This is without a doubt the easiest way to go about such things, but you might find times when it is easier to use the command-line approach.

The command for changing file permissions is chmod (change mode). To use it, just type the command followed by the permissions you want to extend to a file and then the location of the file itself. For example, let’s say you copied a JPEG file, mybirthday.jpg, from a CD to the personal subfolder within the Photos folder on your hard disk, and the file is write protected. To change the file so that you have write permissions (meaning that you can alter the file), you would type the following and then press ENTER:

```
chmod 744 ~/photos/personal/mybirthday.jpg
```

To change the permissions of all the files and subfolders (and all the files within those subfolders) in one fell swoop, you can add the -R (recursive) flag to the chmod command. The command would thus be as follows:

```
chmod -R 744 ~/photos/personal
```

The number 744, by the way, extends read, write, and execute (run) permissions to you, the owner, but gives read-only rights to everyone else—a pretty safe choice when in doubt. If you want to figure out permission numbers for yourself, it is pretty easy. You are basically dealing with three number positions, each of which has eight numerical possibilities (0–7). The left slot represents permissions for the owner, the center slot represents permissions for the group, and the third slot represents permissions for others.

The meanings of the numbers themselves are as follows:

- 7 Read, write, and execute permissions
- 6 Read and write permissions
- 5 Read and execute permissions
- 4 Read-only permissions
- 3 Read and execute permissions
- 2 Write-only permissions
- 1 Execute-only permissions
- 0 No permissions

Figure 9-7 points out the meaning of each of these numbers and what each number slot represents. In fact, if you don’t mind a bit of simple addition, things are even easier to understand. To start with, remember that 1 = execute, 2 = write, and 4 = read. Add any of those numbers together, and you get the other permission combos. For example, 1 (execute) + 4 (read) = 5 (read and execute). As you can see, permissions aren’t all that complicated.

![](img/f7cef0df22f9dba5a41777808c98eece_203_0.png)

Figure 9-7: The meaning of permission numbers

Now if you’re more of a letters than numbers sort of person, you’ll be happy to know that there is another way to change permissions that is probably even easier. In this approach, you have to deal only with two groups of letters and the symbols + and -.
The first group consists of the following:

- u User (owner of the file)
- g Group (specified group of users)
- o Others (anyone who is not the user or a member of the group)
- a All (all of the above)
