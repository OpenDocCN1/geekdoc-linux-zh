# **Using the Input Mode**

By now, you probably know all you ever want to know about *vi* commands. Your sleeves are up and you're ready to plow into inserting text into your page. Before you can tackle this chore, however, you need to know — what else?— a few more *vi* commands.

I begin by showing you the various ways for you to enter the input mode from the command mode. Table B-6 contains the commands that you need to know before you begin typing away.

Table B-6 Entering the Input Mode
| Command | What It Does |
| :--- | :--- |
| A | Places new text after the cursor position. |
| Shift+A | Places new text after the end of the current line. |
| I | Places new text in front of the cursor position. |
| Shift+I | Places new text in front of the current line. |
| 0 | Places new text below the current line at the beginning of the next line. |
| Shift+0 | Places new text on the line above the current line at the beginning of the line. |
| R | Replaces the character at the cursor with the next character that you enter at the keyboard. Typing r'b', for example, replaces the character at the cursor with the letter b. |
| Shift+R | Overwrites the text beginning with the character over the cursor. You can stop overwriting the text by returning to the command mode (by pressing Esc). |
| cw**word**+Esc | Replaces the word at the cursor with another word. If the cursor is on the word **Bob**, for example, and you enter **cw**Mary and press **Esc**, *vi* replaces the word **Bob** with the word **Mary**. |