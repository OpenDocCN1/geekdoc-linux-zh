Because it’s in the PATH, any files you put in ~/bin can be run from the shell prompt without specifying the full path to the file. You could also, of course, create your own directory and manually edit your bash configuration files to add it to your user’s PATH environment variable as well.

With this background in mind, let’s spend some time discussing how to create a basic shell script.

# # Creating a Basic Script

As mentioned earlier, shell scripts can range from extremely basic to extremely complex. The example we reviewed earlier was a very simple script. It echoed text on the screen and ran one command. For your Linux+/LPIC 1 exam, you need to be able to create scripts that are much more complex than this. Therefore, in this part of the chapter, we’re going to cover the following topics:

+   - Displaying text on the screen
+   - Adding commands to a script
+   - Reading input from the user

Let’s begin by discussing how to display text on the screen in a shell script.

# ## Displaying Text on the Screen

This task is pretty easy. As you saw in the earlier examples we reviewed, you can display text on the screen in a shell script using the echo command. The syntax for using echo is to simply enter echo `"text_to_be_displayed"` in the script file.

In the simple script example we looked at earlier, I entered echo "The current date and time:" to display the associated text on the screen. Because the shell script simply calls and runs the echo command, you can use all of the options you would use if you were to run echo at the shell prompt. Check out the man page for echo to see what’s available.

In addition to displaying text on the screen, you can also run commands from the script. Let’s review how this is done next.

# ## Adding Commands to a Script

To run a shell command from within a script, simply enter the appropriate command in the script with all of the options you want to include with it. In the simple script example we looked at earlier, I used the date command to display the current date and time. You can include just about any command you want in your shell scripts. Just remember to put each command on a separate line unless you are using pipes to move data between commands.

Let’s make things a little more interesting by discussing how to gather input from the user in a script.