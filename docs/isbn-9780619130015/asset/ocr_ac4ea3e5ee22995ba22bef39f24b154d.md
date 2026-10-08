# ## Searching and Replacing

Let’s say you want to change all occurrences of “text” in your memo to “documents.” Instead of searching for “text” and then deleting and inserting “documents,” you can search and replace with one command. The commands you learned so far are screen-oriented. Commands that can perform more than one action (searching and replacing) are line-oriented commands.

Note: **Screen-oriented commands** execute at the location of the cursor. You do not need to tell the computer where to perform the operation: it takes place relative to the cursor. Line-oriented commands, on the other hand, require you to specify an exact location (an address) for the operation. Screen-oriented commands are easy to type, and their changes appear on the screen. Typing line-oriented commands is more complicated, but they can execute independently of the cursor and in more than one place in a file.

A colon (:) precedes all line-oriented commands. It acts as a prompt on the status line. Enter line-oriented commands on the status line, and press Enter when you complete the command.

Note: In this chapter, all instructions for line-oriented commands include the colon as part of the command.

**To search for a pattern of characters:**

+   1. Press Esc to make sure you are in command mode.
2. Type /form and press **Enter**. This command instructs vi to search for the first occurrence of the word “form” and moves the cursor under that word.
3. Type n to repeat the search. vi locates the next occurrence of the word “form.”

**To search for “text” and replace it with “documents”:**

+   1. Press Esc to make sure you are in command mode.
2. Type :1,$s/text/documents/g. This command means “From the first line (1) to the end of the file ($), search for ‘text’ and replace it with ‘documents’ (s/text/documents/) everywhere it occurs on each line (g).”
3. Press **Enter**. Your screen should look like the one illustrated in Figure 3-9.