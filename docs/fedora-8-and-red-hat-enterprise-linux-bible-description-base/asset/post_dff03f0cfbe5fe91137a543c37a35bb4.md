
The box at the top represents where your cursor is. The bottom line keeps you informed about what is going on with your editing (here you just opened a new file). In between, there are tildes (~) as filler because there is no text in the file yet. Now here’s the intimidating part: there are no hints, menus, or icons to tell you what to do. On top of that, you can’t just start typing. If you do, the computer is likely to beep at you. And some people complain that Linux isn’t friendly.

The first things you need to know are the different operating modes. The vi editor operates in either command mode or input mode. When you start vi, you are in command mode. Before you can add or change text in the file, you have to type a command to tell vi what you want to do. A command consists of one or two letters and an optional number. To get into input mode, you need to type an input command. To start out, type either of the following input commands:

- a — Add. After you type a, you can input text that starts to the right of the cursor.
- i — Insert. After you type i, you can input text that starts to the left of the cursor.

Type a few words and press Enter. Repeat that a few times until you have a few lines of text. When you are done typing, press Esc. You are now back in command mode. Now that you have a file with some text in it, try moving around in your text with the following keys or letters.

> TIP: Remember the Esc key! It always places you back into command mode.

- Arrow keys — Use the arrow keys to move up, down, left, or right in the file one character at a time. To move left and right you can also use Backspace and the Spacebar, respectively. If you prefer to keep your fingers on the keyboard, use h (left), l (right), j (down), or k (up) to move the cursor.
- w — Moves the cursor to the beginning of the next word.
- b — Moves the cursor to the beginning of the previous word.
- 0 (zero) or ^ — Moves the cursor to the beginning of the current line.
- $ — Moves the cursor to the end of the current line.
- H — Moves the cursor to the upper-left corner of the screen (first line on the screen).
- M — Moves the cursor to the first character of the middle line on the screen.
- L — Moves the cursor to the lower-left corner of the screen (last line on the screen).

Now that you know how to input text and move around, the only other editing you need to know is how to delete text. Here are a few vi commands for deleting text:

- x — Deletes the character under the cursor.
- X — Deletes the character directly before the cursor.
- dw — Deletes from the current character to the end of the current word.
- d$ — Deletes from the current character to the end of the current line.
- d0 — Deletes from the previous character to the beginning of the current line.

If you feel pretty good about creating text and moving around the file, you may want to wrap things up. Use the following keystrokes for saving and quitting the file:

- ZZ — Save the current changes to the file and exit from vi.
- :w — Save the current file but continue editing.
- :wq — Same as ZZ.
- :q — Quit the current file. This works only if you don’t have any unsaved changes.
- :q! — Quit the current file and don’t save the changes you just made to the file.

> **TIP:** If you’ve really trashed the file by mistake, the :q! command is the best way to exit and abandon your changes. The file reverts to the most recently changed version. So, if you just did :w, you are stuck with the changes up to that point. If you just want to undo a few bad edits, press u to back out of changes.

You have learned a few vi editing commands. I describe more commands in the following sections. However, before I do, here are a few tips to smooth out your first trials with vi:

- Esc — Remember that Esc gets you back to command mode. (I’ve watched people press every key on the keyboard trying to get out of a file.) Esc followed by ZZ gets you out of input mode, saves the file, and exits.
- u — Press u to undo the previous change you made. Continue to press u to undo the change before that, and the one before that. (With the traditional vi editor, u undoes a single command and r returns what you just undid.)
- Ctrl+r — If you decide you didn’t want to undo the previous edit, use Ctrl+r for Redo. Essentially, this command undoes your undo.
- Caps Lock — Beware of hitting Caps Lock by mistake. Everything you type in vi has a different meaning when the letters are capitalized. You don’t get a warning if you are typing capitals—things just start acting weirdly.
- :! command — You can run a shell command while you are in vi using :! followed by a command name. For example, type :!date to see the current date and time, type :!pwd to see what your current directory is, or type :!jobs to see if you have any jobs running in the background. When the command completes, press Enter and you are back to editing the file. You could even do that with a shell (:!bash) to run a few commands from the shell, then type exit to return to vi. (I recommend doing a save before escaping to the shell, just in case you forget to go back to vi.)
- INSERT — When you are in input mode, the word INSERT appears at the bottom of the screen. Other messages also appear at the line at the bottom of the screen.
- Ctrl+g — If you forget what you are editing, pressing these keys displays the name of the file that you are editing and the current line that you are on. It also displays the total number of lines in the file, the percentage of how far you are through the file, and the column number the cursor is on. This just helps you get your bearings after you've stopped for a cup of coffee at 3 a.m.

## Moving around the file

Besides the few movement commands described earlier, there are other ways of moving around a vi file. To try these out, open a large file that you can't do much damage to. (Try copying /var/log/messages to /tmp and opening it in vi.) Here are some movement commands you can use:

- Ctrl+f — Page ahead, one page at a time.
- Ctrl+b — Page back, one page at a time.
- Ctrl+d — Page ahead a half page at a time.
- Ctrl+u — Page back a half page at a time.
- G — Go to the last line of the file.
- gg or 1G — Go to the first line of the file. (Use any number with a G or gg to go to that line in the file.)

## Searching for text

To search for the next occurrence of text in the file, use either the slash (/) or the question mark (?) character. Within the search, you can also use metacharacters. Here are some examples:

- /hello — Searches forward for the word hello.
- ?goodbye — Searches backward for the word goodbye.
- /The .*foot — Searches forward for a line that has the word The in it and also, after that at some point, the word foot.
- ?[pP]rint — Searches backward for either print or Print. Remember that case matters in Linux, so using brackets can search for words that could have different capitalization.

The vi editor was originally based on the ex editor. That editor did not let you work in full-screen mode. However, it did enable you to run commands that let you find and change text on one or more lines at a time. When you type a colon and the cursor goes to the bottom of the screen, you are essentially in `ex` mode. Here is an example of some of those `ex` commands for searching for and changing text. (I chose the words *Local* and *Remote* to search for, but you can use any appropriate words.)

- `:g/Local` — Searches for the word *Local* and prints every occurrence of that line from the file. (If there is more than a screenful, the output is piped to the `more` command.)
- `:s/Local/Remote` — Substitutes *Remote* for the word *Local* on the current line.
- `:g/Local/s//Remote` — Substitutes the first occurrence of the word *Local* on every line of the file with the word *Remote*.
- `:g/Local/s//Remote/g` — Substitutes every occurrence of the word *Local* with the word *Remote* in the entire file.
- `:g/Local/s//Remote/gp` — Substitutes every occurrence of the word *Local* with the word *Remote* in the entire file, then prints each line so that you can see the changes (piping it through `more` if output fills more than one page).

## Using numbers with commands

You can precede most `vi` commands with numbers to have the command repeated that number of times. This is a handy way to deal with several lines, words, or characters at a time. Here are some examples:

- `3dw` — Deletes the next three words.
- `5cl` — Changes the next five letters (that is, removes the letters and enters input mode).
- `12j` — Moves down 12 lines.

Putting a number in front of most commands just repeats those commands. At this point, you should be fairly proficient at using the `vi` command. If you would like further instruction, I suggest you try the *VIM Tutor* by running the `vimtutor` command.

> **NOTE:** When you invoke `vi` on Fedora or RHEL, you're actually invoking the `vim` text editor, which runs in `vi` compatibility mode. Those who do a lot of programming might prefer `vim`, because it shows different levels of code in different colors. `vim` has other useful features, such as the ability to open a document with the cursor at the same place where it was when you last exited that file.

## Summary

Working from a shell command-line interpreter within Linux may not be as simple as using a GUI, but it offers many powerful and flexible features. This chapter describes how to log in to Fedora or RHEL and use shell commands. Features for running commands include recalling commands from a history list, completing commands, and joining commands.
