# **EXERCISE 1.1** _(continued)_

+   5. Type `1s -l t`, and without pressing the Enter key, press the Tab key. The system may beep at you or display two `three`. If it doesn't display two `three`, press the Tab key again, and it should do so. This reveals that either two or three is a valid completion to your command, because these are the two files in the test directory whose file-names begin with the letter `t`.
+   6. Type `h`, and again without pressing the Enter key, press the Tab key. The system should complete the command `1s -l three`, at which point you can press the Enter key to execute it. (You'll see information on the file.)
+   7. Press the Up arrow key. You should see the `1s -l three` command appear on the command line.
+   8. Press Ctrl+A to move the cursor to the beginning of the line.
+   9. Press the Right arrow key once, and type `es` (without pressing the Enter key). The command line should now read `less -l three`.
+   10. Press the Right arrow key once, and press the Delete key three times. The command should now read `less` `three`. Press the Enter key to execute the command. (Note that you can do so even though the cursor isn't at the end of the line.) This invokes the `less` pager on the `three` file. (The `less` pager is described more fully later, in “Getting Help.”) Because this file is empty, you'll see a mostly empty screen.
+   11. Press the Q key to exit from the `less` pager.

# ## Exploring Shell Configuration

Shells, like many Linux programs, are configured through files that hold configuration options in a plain-text format. The bash configuration files are actually bash shell scripts, which are described more fully in Chapter 9. For now, you should know that the `~/.bashrc` and `~/profile` files are the main user configuration files for bash, and `/etc/bash.bashrc` and `/etc/profile` are the main global configuration files.

Even without knowing much about shell scripting, you can make simple changes to these files. Edit them in your favorite text editor, and change whatever needs changing. For instance, you can add directories to the $PATH environment variable, which takes a colon-delimited list of directories.