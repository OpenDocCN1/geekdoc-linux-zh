is the location where it is to be pasted (*command_exp/*). After you try it out, have a look within your *command_exp* folder to make sure the file you copied is there.

So what happens if the file you want to copy isn’t in your Home folder? Say, for example, your *tawas.png* file is in the *command_exp* folder, and you want to place a copy of it in a *happy_pics* folder that is also located in the *command_exp* folder. Well, you actually have a couple of ways of going about it.

One way is to first use the cd command you just learned to move into the *command_exp* folder. You then type `cd command_exp`, and then press **ENTER**, which places you in the *command_exp* folder. You then use the `cp` command to copy the *tawas.png* file and paste it in the *happy_pics* folder by typing `cp tawas.png happy_pics/` and then pressing **ENTER**.

The second alternative is to do it all in one fell swoop using only the `cp` command. To go this route, type `cp command_exp/tawas.png command_exp/happy_pics/` and then press **ENTER**. This route is equally effective, although it involves a tad more typing.

# $ rm

The `rm` (remove) command, as its name implies, is used to remove files and empty folders—a sort of command-line version of moving things to Trash. The `rm` command, albeit very useful and easy to use, should be used with caution. Once you remove a file with this command, there is no going back—the file is gone for good.

To play it safe, let’s try out the `rm` command by getting rid of that new copy of the file you moved to the *command_exp* folder moments ago. The basic `rm` command structure consists of the command itself, `rm`, followed by the name of the file that you want to remove. Assuming your Console shows you to be Home, you can remove the file by typing `rm command_exp/` followed by a tap on the `⏎ ENTER` key. The file will then be gone, and gone for good.

If the file is not in the Home folder, just use the `cd` command to move into the folder in which it is placed, and then use the `rm` command once there. As with the `cp` command, you can achieve the same thing in one go by typing `rm foldername/filename` and pressing **ENTER**.

Now that we are essentially finished with the experimentation process, you might as well get rid of the *command_exp* folder. However, since that folder has a subfolder (sub) within it, the `rm` command cannot handle the job. This is because, as I mentioned before, the *command can be used only to remove files and empty folders*. To remove a folder and its contents as well, you need to add the recursive flag, `r`. To do this, just type `rm -r command_exp` and then press **ENTER**. Your *command_exp* folder and the subfolder within will then be but a memory.