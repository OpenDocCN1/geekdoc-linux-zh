Better. It is now easier to differentiate between the shell prompt and the text that we are trying to read. It would be even better if we could clearly separate this text from the shell prompt above and the shell prompt below. We can do that by pressing the `<Enter>` key twice.

+   8. Create the file `tempfile3`.
+       a. Type `cat > tempfile3`
+       b. Press `<Enter>` to get the system to respond to the command line above.
+       c. Press `<Enter>` to create a blank line at the start of the file.
+       d. Type: `This is tempfile3`.
+       e. Press `<Enter>` to move the cursor to the next line.
+       f. Press `<Enter>` to create a blank line at the end of the file.
+       g. Press `<Ctrl-D>`

+   9. Read `tempfile3`.
+       a. Type `cat tempfile3`
+       b. Press `<Enter>`

Your screen will look similar to Figure 6-5.

![](bbox=[0.18, 0.55, 0.84, 0.67])

**Figure 6-5** Text of `tempfile3` Clearly Separated from Shell Prompt

You can see the text of `tempfile3` clearly separated from our expanded shell prompts.

On some systems, there may be a lag between the time you issue a command to create or save a file and the time that the system actually stores the file on the disk itself. While this is not something you normally need to be concerned about, there will undoubtedly be a time when you have created a very important file and you want to be certain that file is stored on the disk. At that moment, you will want to use the `sync` command.