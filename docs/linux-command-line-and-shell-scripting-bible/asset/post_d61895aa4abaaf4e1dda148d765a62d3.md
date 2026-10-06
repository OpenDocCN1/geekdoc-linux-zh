
# The Linux Command Line

To continue searching for the same word, press the forward slash character, press the Enter key, or you can use the n key, for next.

The substitute command allows you to quickly replace (substitute) one word for another in the text. To get to the substitute you must be in command mode. The format for the substitute command is:

```
:s/new/
```

The vim editor jumps to the first occurrence of the old text and replaces it with the new text. There are a few modifications you can make to the substitute command to substitute more than one occurrence of the:

- :s/old/new/g to replace all occurrences of old in a line
- :#/s/old/new/g to replace all occurrences of old between two lines numbers
- %s/old/new/g to replace all occurrences of old in the entire file
- %s/old/new/gc to replace all occurrences of old in the entire file, but prompt for all occurrence

As you can see, for a command line editor, vim contains quite a few advanced features. Since every Linux distribution includes it, it's a good idea to at least know the basics of the vim editor so that you can easily edit scripts, no matter where you are or what you have available.

## The emacs Editor

The emacs editor is an extremely popular editor that appeared before even Unix was around. Developers liked it so much that they ported it to the Unix environment, and now it's ported to the Linux environment. The emacs editor started life as a console editor, much like vi, but has made the migration to the graphical world.

The emacs still provides the original console mode editor, but now it also has the ability to use a graphical Windows window for editing text in a graphical environment. Normally, when you start emacs editor from a command line, it will determine if you have an X Window session and start in graphical mode. If you don't, it'll start in console mode.

This section describes both the console mode and graphical mode editors so that you'll know how to use one if you want (or need).

### Using emacs on the console

The console mode version of emacs is another editor that uses lots of key commands to perform editing functions. The emacs editor uses key combinations pressing the Control key (Ctrl on keyboard) and the Meta key. In most PC terminal emulator packages, the Meta key is mapped to the PC's Alt key. The official emacs documents abbreviate the Ctrl key as C- and the Meta key as M-. Thus, if you enter a Ctrl-x key combination, the document shows C-x. I'll do the same here so as not to confuse you.

# Working with Editors

FIGURE 7-2

Editing a file using the emacs editor in console mode

![](img/adcbcf1053b52dbf22f3aa187738232f_208_0.png)

# The basics of emacs

To edit a file using emacs, from the command line, enter:

$ emacs myprog.c

The emacs console window appears with a short introduction and help screen. Don't be alarmed; as soon as you press a key, emacs loads the file into the active buffer and displays the text, as shown in Figure 7-2.

You'll notice that the top of the console window shows a typical menubar. Unfortunately, you won't be able to use the menubar in console mode, or in graphical mode.

Unlike the editor, where you have to move in and out of insert mode to switch between entering commands and inserting text, the emacs editor only has one mode. If you type a printable character, emacs inserts it at the current cursor position. If you type a command, emacs executes the command.

To move the cursor around the buffer area, you can use the arrow keys and the PageUp and PageDown keys, assuming that emacs detected your terminal emulator correctly. If not, there are commands for moving around the cursor around:

- C-p to move up one line (the previous line in the text).
- C-b to move left (back) one character.

- C-f to move right (forward) one character.
- C-n to move down one line (the next line in the text).

There are also commands for making longer jumps with the cursor within the text:

- M-f moves right (forward) to the next word.
- M-b moves left (backward) to the previous word.
- C-a moves to the beginning of the current line.
- C-e moves to the end of the current line.
- M-a moves to the beginning of the current sentence.
- M-e moves to the end of the current sentence.
- M-v moves back one screen of data.
- C-v moves forward one screen of data.
- M-< to move the first line of the text.
- M-> to move to the last line of the text.

There are several commands you should know for saving the editor buffer back into the file, and exiting emacs:

- C-x C to save the current buffer contents to the file.
- C-z to exit emacs but keep it running in your session so that you can come back to it.
- C-x C-c to exit emacs and stop the program.

You'll notice that these two features require two commands. The C-x command is called the *extend command*. This provides yet another set of commands to work with.

# Editing data

The emacs editor is pretty robust about inserting and deleting text in the buffer. To insert text, just move the cursor to the location where you want to insert the text and start typing. To delete, emacs uses the Backspace key to delete the character before the current cursor position and the Delete key to delete the character at the current cursor location.

The emacs editor also has commands for killing text. The difference between deleting text and killing text is that when you kill text, emacs places it in a temporary area where you can retrieve (see the "Copying and pasting" section). Deleted text is gone forever.

There are a few for killing text in the buffer:

- M-Backspace to kill the word before the current cursor position.
- M-d to kill the word after the current cursor position.
- C-k to kill from the current cursor position to the end of the line.
- M-k to kill from the current cursor position to the end of the sentence.

The emacs editor also includes a fancy way of mass-killing. Just move the cursor to the start of the area you want to kill, and press either the C-@ or C-Spacebar keys. Move the cursor to the end of the area you want to kill and press the C-w command keys. All of the text between the two locations is killed.

If you happen to make a mistake when killing text, the C-u command will undo the kill command, and return the data it was before you killed it.

# Copying and pasting

You've seen how to cut from the emacs buffer area; now it's time to see how to paste it somewhere. Unfortunately, if you use the vim editor, this process may confuse you when you use the emacs editor.

In an unfortunate coincidence, pasting data in emacs is called yank. In the vim editor, copying is called yank, which is makes this a difficult thing to remember if you happen to use both editors.

After you kill data using one of the kill commands, move the cursor to the location where you want to paste the data, and use the C-y command. This yanks the text out of the temporary area and pastes it at the current cursor position. The C-y command yanks the text from the last command. If you performed multiple kill commands, you can cycle through them using the M-y command.

To copy, just yank back into the same location you killed it, then move to the new location and use the C-y command again. You can yank back as many times as you desire.

# Searching and replacing

Searching in the emacs editor is done by using the C-s and C-r commands. The C-s command performs a forward search in the buffer area from the current cursor position to the end of the buffer, where the C-r performs a backward search in the buffer area from the start of the buffer.

When you enter either the C-s or C-r command, a prompt appears in the bottom line, querying you for the text to search. There are two types of searches that emacs can perform.

In an incremental search, the emacs editor performs the text search in real-time mode as you type the word. When you type the first letter, it highlights all the occurrences of that letter in the buffer. When you type the second letter, it highlights all the occurrences of the two letter combination in the text, and so until you complete the text you're searching for.

In a non-incremental search, press the Enter key after the C-s or C-r commands. This locks the search query into the bottom line area and allows you to type the search text in full.

To replace an existing text with a new text, you have to use the M-x command. This requires a text command, along with parameters.
