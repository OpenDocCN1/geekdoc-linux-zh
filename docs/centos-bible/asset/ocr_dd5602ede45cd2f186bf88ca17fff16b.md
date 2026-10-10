# Getting Started

+   - `?goodbye` — Searches backward for the word *goodbye*.
+   - `/The.*foot` — Searches forward for a line that has the word *The* in it and also, after that at some point, the word *foot*.
+   - `?[pP]rint` — Searches backward for either *print* or *Print*. Remember that case matters in Linux, so using brackets can search for words that could have different capitalization.

The vi editor was originally based on the ex editor. That editor did not let you work in Full-Screen mode. However, it did enable you to run commands that let you find and change text on one or more lines at a time. When you type a colon and the cursor goes to the bottom of the screen, you are essentially in ex mode. Here is an example of some of those ex commands for searching for and changing text. (I chose the words *Local* and *Remote* to search for, but you can use any appropriate words.)

+   - `:g/Local` — Searches for the word *Local* and prints every occurrence of that line from the file. (If there is more than a screenful, the output is piped to the `more` command.)
+   - `:s/Local/Remote` — Substitutes *Remote* for the word *Local* on the current line.
+   - `:g/Local/s//Remote` — Substitutes the first occurrence of the word *Local* on every line of the file with the word *Remote*.
+   - `:g/Local/s//Remote/g` — Substitutes every occurrence of the word *Local* with the word *Remote* in the entire file.
+   - `:s/Local//Remote/gp` — Substitutes every occurrence of the word *Local* with the word *Remote* in the entire file, then prints each line so you can see the changes (piping it through `more` if output fills more than one line). Another way to globally search and replace without printing every line that changes is to type `:%s/Local/Remote/g`.

# Using Numbers with Commands

You can precede most vi commands with numbers to have the command repeated that number of times. This is a handy way to deal with several lines, words, or characters at a time. Here are some examples:

+   - `3dw` — Deletes the next three words.
+   - `5c}` — Changes the next five letters (*i.e.,* removes the letters and enters input mode).
+   - `12]` — Moves down 12 lines.

Putting a number in front of most commands just repeats those commands. At this point, you should be fairly proficient at using the vi command. If you would like further instruction, I suggest you try the VIM Tutor by running the `vimtutor` command.

> > **NOTE** When you invoke `vi` on CentOS, you’re actually invoking the *vim* text editor, which runs in *vi* compatibility mode. Those who do a lot of programming might prefer *vim*, because it shows different keywords or code in different colors. *vim* also has other useful features, such as the ability to open a document with the cursor at the same place where it was when you last exited that file.