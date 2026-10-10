
was launched, but it shares that display with the shell. This works well for noninteractive programs but very poorly for interactive tools. For instance, suppose you have a program called **supercrunch** that performs some lengthy computation but requires no interaction from the user. You could launch it like this:

```
$ supercrunch &
```

If **supercrunch** produces text-based output, it will appear on the screen, but you’ll still be able to use the shell for other purposes. If you’ve already launched a program and want to move it into the background, press **Ctrl+Z**. This suspends the currently running program and returns you to the shell. At this point, the program you’ve suspended will not be doing any work. This may be fine for a text editor you wanted to momentarily suspend, but if the program was performing computations that should continue, you must take additional steps to see that this happens. You can type **fg** to return to the suspended program or type **bg** to start it running again in the background. The latter is much like appending an ampersand to the command name when you launched it.

If you try to launch an X-based program, you must be running the shell in an **xterm**, or possibly in some other way that allows X programs to run, such as from another Computer with its own X server and all appropriate environment variables set to permit remote X program operation, as described in Chapter 9, “Configuring Advanced Networking.” If you try to launch an X program from a text-only login, you’ll receive an error message along the lines of `Can’t open display`.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_90_0.png)

> Although X-based programs don’t normally produce text output, they do take over the terminal from which they were launched. If you want to continue to use a terminal after launching an X-based program, follow its name with an ampersand (&), as just described.

## Using Shell Shortcuts

Linux shells permit some important shortcuts. One of these is the use of the Tab key for **filename completion**. Suppose you want to move a file that’s called **shareholder-report-for-2009.txt**. You could type the entire filename, but that can be tedious. Most Linux shells, including the popular **Bash**, support a feature in which hitting the Tab key completes an incomplete command or filename, as long as you’ve typed enough characters to uniquely define the file or command. For instance, suppose that **ls** (described in more detail shortly, in “Listing Files”) reveals two files in a directory:

```
$ ls
share-price-in-2009.txt  shareholder-report-for-2009.txt
```

If you want to edit the second file with the Emacs editor (using the command name **emacs**), you could type **emacs shareh** and then press the Tab key. The shell will complete the filename.

What happens when the characters you enter are *not unique*? In this case, the shell completes as much of the job as it can. For instance, if you type `emacs` *sh* and then press the Tab key, Bash fills out the next three characters so that the command line reads `emacs share`. Some configurations also summarize the possible completions at this point. (For those that don’t, pressing Tab again usually displays these completions.) If you then type either **h** or **-** and press Tab again, Bash completes the filename.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_91_0.png)

Another shortcut is the use of the up and down arrow keys to scroll through previous commands. If you need to type two similar commands in a row, you can type one and then press the up arrow key to retrieve the previous command. You can go back through several commands in this way, and if you overshoot, you can use the down arrow key to retrieve more recent commands. Once you find the command you want, you can use the left arrow or Backspace key to move back in the line to edit it (Backspace deletes characters, but the left arrow key doesn’t). Pressing Ctrl+A moves the cursor to the start of the line, and pressing Ctrl+E moves the cursor to the end of the line. Edit the line, and press the Enter key to enter the new command.

These shortcuts, and other basic shell commands, are extremely helpful. You can perform many tasks with a file manager, of course, but text-based utilities were designed to be used from shells.

## Using the Shell’s History

Another helpful shell shortcut is the *history*, which keeps a record of every command you type (stored in `~/.bash_history` in the case of Bash), up to a configurable number of commands. If you’ve typed a long command recently and want to use it again, or use a minor variant of it, you can pull the command out of the history. The simplest way to do this is to press the up and down arrow keys on your keyboard, as described in the previous section. The Ctrl+P and Ctrl+N keystrokes double for the up and down arrow keys, respectively.

Another way to use the command history is to search through it. Press Ctrl+R to begin a backward (reverse) search, and begin typing characters that should be unique to the command you want to find. The characters you type need not be the ones that begin the command; they can exist anywhere in the command. You can either keep typing until you find the correct command or, after you’ve typed a few characters, press Ctrl+R repeatedly until you find the one you want. The Ctrl+S keystroke works similarly but searches forward in the command history, which might be handy if you’ve used a backward search or the up arrow key to look back and have overshot. In either event, if you can’t find the command you want or change your mind and want to terminate the search, press Ctrl+G.

Frequently, after finding a command in the history, you want to edit it. Bash, like many shells, provides editing features modeled after those of the Emacs editor:

- **Move within the line.** Press Ctrl+A or Ctrl+E to move the cursor to the start or end of the line, respectively. The left and right arrow keys move within the line a character at a time. Ctrl+B and Ctrl+F do the same, moving backward and forward within a line. Pressing Ctrl plus the left or right arrow key moves backward or forward a word at a time, as does pressing Esc and then B or F.

- **Delete text.** Pressing Ctrl+D or the Delete key deletes the character under the cursor, whereas pressing the Backspace key deletes the character to the left of the cursor. Pressing Ctrl+K deletes all text from the cursor to the end of the line. Pressing Ctrl+X and then Backspace deletes all the text from the cursor to the beginning of the line.

- **Transpose text.** Pressing Ctrl+T transposes the character before the cursor with the character under the cursor. Pressing Esc and then T transposes the two words immediately before (or under) the cursor.

- **Change case.** Pressing Esc and then U converts text from the cursor to the end of the word to uppercase. Pressing Esc and then L converts text from the cursor to the end of the word to lowercase. Pressing Esc and then C converts the letter under the cursor (or the first letter of the next word) to uppercase, leaving the rest of the word unaffected.

- **Invoke an editor.** You can launch a full-fledged editor to edit a command by pressing Ctrl+X followed by Ctrl+E. Bash attempts to launch the editor defined by the FCEDIT or EDITOR environment variable or Emacs as a last resort. (The upcoming section “Setting Environment Variables” describes environment variables.)

These editing commands are just the most useful ones supported by Bash; consult its man page to learn about many more obscure editing features. In practice, you're likely to make heavy use of command and filename completion, the command history, and perhaps a few editing features.

The **history** command provides an interface to view and manage the history. Typing **history** alone displays all the commands in the history (typically the latest 500 commands); adding a number causes only that number of the latest commands to appear. Typing **history -c** clears the history, which can be handy if you've recently typed commands you'd rather not have discovered by others (such as commands that include passwords). You can rerun a specific command by typing its number preceded by an exclamation mark (!), as in !227 to rerun the command that's numbered 227 in the list.

# Manipulating Files and Directories

Linux provides traditional Unix commands to manipulate files. These commands can be classified into several categories: filesystem navigation, file manipulation, directory manipulation, file location, and file comparison. A couple of closely related features are redirection and pipes, which let you redirect a program's input or output from or to a file or another program.
