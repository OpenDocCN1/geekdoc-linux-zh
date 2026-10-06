# CONTROL-Z Suspends a Program

Although not a way of correcting a mistake, you may press the suspend key (typically CONTROL-Z) by mistake and wonder what happened (you will see a message containing the word Stopped). You have just stopped your job, using job control (page 554). Give the command fg to control your job in the foreground, and you should be back to where you were before you pressed the suspend key. Although not usual, it is possible to change the suspend key (page 1339). For more information, refer to "bg: Sends a Job to the Background" on page 556.

If you would like to use another key as your erase key, refer to "Examples" on page 1338. You can use any key you like, but some choices are more convenient than others.

# Delete a Word

In shells you can delete a word by pressing CONTROL-W. A word is any sequence of characters that does not contain a SPACE or TAB. When you press CONTROL-W, the cursor moves to the beginning of the current word (as you are entering a word) or the previous word (when you have just entered a SPACE or TAB), moving the word. The stty utility uses werase for controlling the character that performs this function (page 1336).

# Delete a Line

Any time before you press RETURN, you can delete a line you are entering by pressing the line kill key, or kill key. When you press this key, the cursor moves to the left, erasing characters as it goes, back to the beginning of the line. The default line key is CONTROL-U. If this does not work, try CONTROL-X. If these keys do not work, give the following command to erase and reset line keys to their defaults:

+   $ stty ek

If you would like to use another key as your line kill key, refer to "Examples" on page 1338.

# Abort Execution

Sometimes you may want to terminate a running program. A GNU/Linux program may be performing a lengthy task such as displaying the contents of a file that is several hundred pages or copying a file that is not the one you meant to copy.

To terminate a program from a character-based display, press the interrupt key (CONTROL-C or sometimes DELETE or DEL). When you press this key, the GNU/Linux operating system sends a terminal interrupt signal to the program you are running and