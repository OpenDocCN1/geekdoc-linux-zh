# 74 Part I ♦ Linux First Steps

+   - command — You can run a command while you are in vi :! followed by a command name. For example, type :date to see the current date and time, type :pwd to see your current directory, or type :jobs to see if you have any jobs running in the background. When the command completes, press Enter and you are back to editing the file. You could even use this technique to launch a shell (:bash) from vi, run a few commands from that shell, and then type exit to return to vi. (I recommend saving a safe before escaping to the shell, in case you forget to go back to vi.)

+   - INSERT—When you are in insert mode, the word INSERT appears at the bottom of the screen.

+   - Ctrl+G—If you are editing a file, pressing these keys displays the name of the file that you are editing and the current line that you are on the bottom of the screen. It also displays the total number of lines in the file, the percentage of how far you are from the file, and the column number the cursor is on. This helps you get your bearings after you've stopped for a cup of coffee at 3 a.m.

# Moving Around the File

Besides the few movement commands described earlier, there are other ways of moving around a file. To try these out, open a large file that you can't much damage to. (Try copying /var/log/messages to /tmp and opening it in vi.) Here are some movement commands you can use:

+   - Ctrl+F—Page ahead, one page at a time.

+   - Ctrl+B—Page back, one page at a time.

+   - Ctrl+D—Page ahead one-half page at a time.

+   - Ctrl+U—Page back one-half page at a time.

+   - G—Go to the last line of the file.

+   - IG—Go to the first line of the file. (Use any number to go to that line in the file.)

# Searching for Text

Search for the next occurrence of text in the file, use either the slash (/) or the question mark (?). Follow the slash or question mark with a pattern (string of text) to search forward or backward, respectively, for that pattern. Within the search, you can also use metacharacters. Here are some examples:

+   /hello—Searches forward for the word hello.

+   ?goodbye—Searches backward for the word goodbye.