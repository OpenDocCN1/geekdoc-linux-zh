
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

## Quitting emacs

At this time, you can stop editing to save the contents of the buffer to your file asong2. To do this, issue the command sequence Ctrl+x Ctrl+s. As you enter this command, notice how the command displays on the echo line as you type it. To quit emacs and return to the shell, enter the command Ctrl+x Ctrl+c. If you make changes that haven't been saved using Ctrl+x Ctrl+s, emacs will ask for confirmation before quitting.

## Deleting Text

You can delete text in several ways. The Backspace (or Delete) key is used to erase the character that precedes the cursor. The command Ctrl+d deletes the character underneath the cursor, and Ctrl+k deletes, or "kills," all characters from the cursor to the end of the line. Words can be deleted also: META+d deletes the word the cursor is currently located over, and META+Del (the Delete key) deletes the word just before the current word.

If you ever find that you have done an edit that you didn't want, simply press Ctrl+u to undo the previous editing changes.

> **Tip**
> Change your mind about a command? Press Ctrl+g to abort the current command operation.

## Working with Multiple Files

emacs enables you to edit several files in one session, each contained within its own buffer. To copy an external file into a new buffer, use the Ctrl+x Ctrl+f command. After entering this command, you see the following prompt on the echo line:

Find file: ~/

emacs is smart when it looks for files. It supports *filename completion*, which means that you can simply type a few characters of a filename, and emacs attempts to match a file (or files) to whatever you have typed so far. To do this, type `.log` and press the Tab key. emacs expands this to `~/.login`, and you can see your `.login` file in a new buffer by pressing Return. If two or more files match the pattern supplied, pressing the Tab key cycles through them.

After you load a new file into emacs, you can switch between buffers by using the Ctrl+x b command followed by the name of the buffer that you want. The buffer’s name is that of the file that was loaded into it. The Ctrl+x b command also uses *filename completion*, so you can use the Tab key to cycle through your edit buffers after supplying a few relevant characters.

When you finish editing a buffer, instead of saving the contents by using the Ctrl+x Ctrl+s command, you might decide that you do not really want to keep the edits that you made. You can kill the current buffer by entering the command Ctrl+x k. emacs then prompts you for the name of the buffer to kill, but by simply pressing Return, you can kill the current buffer. Next, emacs asks for confirmation to which you can respond by typing *yes* (if you’re sure) and pressing Return.

> **Tip**
> Whenever you are working with just two buffers, you can simply press Return after entering the Ctrl+x b command to switch to the other buffer.

## Copying and Moving Text

In order to copy and move blocks of text in *emacs*, you must define the region of text by marking the beginning and end points of the text block. This is done by moving the cursor to where you want the block to begin and marking it using the Ctrl+Space command (in this case, Space means literally pressing the spacebar). The end of the block is defined by wherever you place the cursor after that. To make a copy of the block, enter the command META+w. The text within the block is copied to *emacs*'s internal clipboard from which it can be pasted at another location using the Ctrl+y command. Alternatively, you can cut the block into the clipboard using Ctrl+w instead of META+w. Cutting, of course, deletes the text from its current location.

Let's try out some of these techniques on your buffer *asong2*. Use the META+< command to jump to the beginning of the buffer. Enter a Ctrl+Space to mark the start of the block and then use Ctrl+n to move down a line. Cut the block to the clipboard using Ctrl+w, move the cursor to the end of the buffer using META+>, and paste it using Ctrl+y. The result is something like this:

```
It's really quite swell
And all you have to do is spell
emacs works, if you let it!
This is a file for edit
And you have to give emacs some credit
```

## Searching and Replacing Text

You can search forward and backward through text using the Ctrl+s and Ctrl+r commands, respectively. These commands, like many in *emacs*, use *command completion*. This is the same concept as filename completion: you supply a few characters, and *emacs* tries to fill in the rest. In this case, however, *emacs* moves the cursor to each instance it finds of the string supplied.

As you enter more characters, *emacs* narrows its search further. When you have found a correct match, press Return or use any of the cursor-movement commands to halt the search.

As with *vi*, searching in either direction wraps around the beginning or end of the file, depending on in which direction you are searching. However, when *emacs* reaches the top or bottom of the file, it tells you that the search failed. You can keep searching by pressing Ctrl+s or Ctrl+r accordingly, and *emacs* will continue using the current string.

To illustrate how searching in *emacs* works, let's search backward through your file *asong2*. Enter Ctrl+r and type an s. *emacs* moves the cursor to the “s” in “works.” Next type a w. *emacs* now tries to find a pattern that matches the string sw. The cursor ends up on the “w” in “swell.” You can edit the search string by using the Backspace, or Delete, key. Delete the w and type a p. What happens?

Searches-and-replaces are done by entering the query-replace command. This is qualified by the META-x command, which tells emacs that the text to follow is a full command and not a key combination. After you enter the query-replace command, emacs prompts you for the string to be found. Enter the string and press Return. emacs then prompts you for the replacement string. After you enter the replacement string, emacs searches for every instance of the first string and, if it finds one, asks if it should be replaced with the second string.

# Using Modes with Buffers

emacs is versatile enough to handle many different types of editing chores. It enables you to associate modes to buffers so that you can have text formatting specific to your editing application. If you enter the command Ctrl+x m, emacs enters mail mode that formats a buffer with To: and Subject: fields, as well as a space for the body of the mail message. emacs can even send the mail message for you (by entering Ctrl+c Ctrl+c) after you finish editing it.

emacs also supports modes for many different programming languages, such as C. When a file with the extension .c (C source code) or .h (C header file) is loaded into emacs, the buffer is automatically set to C mode. This mode has knowledge of how C programs are formatted, and pressing the Tab key indents a line correctly based on its place in the program (a for loop within another for loop, as an example).

# Online Help in emacs

One of the best features of the emacs editor is that if you ever get stuck or are just plain overwhelmed by it all, help is just a few keystrokes away—and lots of it! If you need a short emacs tutorial, just enter Ctrl+h t. If you need to find out what function a particular key supports, type Ctrl+h k and then press the key. The help option has many different topics. Use Ctrl+h i to load the info documentation reader and read about all the types of help available.

# A Summary of Essential Commands

emacs, like the vi editor, has such a rich command set that we can cover only a portion of it in this chapter. Table 16.2 is a summary of the strictly essential commands that you need for basic editing in emacs. The emacs man page should be consulted for a more comprehensive description of the full emacs command set.

![](img/e8e6b47ac20475e23d48b4c476f5d891_354_0.png)
