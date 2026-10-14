⇒ To insert a line of text in Vi and then move to command mode, type:
    i Hello, world. RET
    ESC

This moves from command mode to insert mode, inserts the text "Hello, world." and a newline character in the current file, where the cursor was, and then brings Vi back to command mode.

The command to get help is :help, and to get a list of commands and their usage, run the :viusage command.

⇒ To get a list of Vi commands and their usage, type:
    :viusage RET

When you open a file in Vi, the content of the file is placed in its own buffer, as with Emacs. Changes are not made to a file on disk until you write them.

To write a buffer to a file, use :w and give the name of the file to write to. Use :wq instead to write the file to disk and quit, and use :q! to abandon all unsaved editing, and quit Vi.

⇒ Here are two ways to use this.

+   - To write the contents of the buffer to the file my_practice_file, and then exit Vi, type:
+     :wq my_practice_file RET
+   - To abandon any unsaved editing and exit Vi, type:
+     :q! RET

**NOTES:** You can also type ZZ to write the changes to the current file and exit.

# 10.2.2 Running a Vi Tutorial

The Vi editor comes with a hands-on, self-paced tutorial that you can run through in under an hour. As with the Emacs tutorial, it's simply a read-only text file that is opened Vi. It's designed to teach you how to use Vi by showing you the various commands and their effects on the text. It's stored as a compressed file in the /usr/doc/nvi directory; copy this file to your home directory, uncompress it, and open it with vi to start the tutorial.