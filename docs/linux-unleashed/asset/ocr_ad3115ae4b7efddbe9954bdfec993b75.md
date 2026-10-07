Most implementations of emacs conveniently map the first four movement commands to the arrow keys on the keyboard. Let's edit a new file called asong2. Start emacs by entering the following command from the shell:
`emacs asong2<Enter>`

Now enter the following text into the buffer:
This is a file for edit
And you have to give emacs some credit
It's really quite swell
And all you have to do is spell
emacs works, if you let it!

Now use the Ctrl+b command to move back through this lovely piece of poetry. Notice how the cursor jumps to the end of each line after reaching the beginning of the previous line. This works the same way in the opposite direction using the Ctrl+f command.

Another useful way of moving around is by scrolling through a file one screen at a time. The command Ctrl+v moves the cursor forward one screen at a time. The command META+v moves the cursor in the opposite direction.

Like vi, emacs treats a sequence of non-whitespace characters as a word. You can move the cursor forward one word at a time with the META+f command. The META+b command moves back one word.

# ## Quitting emacs

At this time, you can stop editing to save the contents of the buffer to your file asong2. To do this, issue the command sequence Ctrl+x Ctrl+s. As you enter this command, notice how the command displays on the echo line as you type it. To quit emacs and return to the shell, enter the command Ctrl+x Ctrl+c. If you make changes that haven't been saved using Ctrl+x Ctrl+s, emacs will ask for confirmation before quitting.

# ## Deleting Text

You can delete text in several ways. The Backspace (or Delete) key is used to erase the character that precedes the cursor. The command Ctrl+d deletes the character underneath the cursor, and Ctrl+k deletes, or "kills," all characters from the cursor to the end of the line. Words can be deleted also: META+d deletes the word the cursor is currently located over, and META+Del (the Delete key) deletes the word just before the current word.

If you ever find that you have done an edit that you didn't want, simply press Ctrl+u to undo the previous editing changes.