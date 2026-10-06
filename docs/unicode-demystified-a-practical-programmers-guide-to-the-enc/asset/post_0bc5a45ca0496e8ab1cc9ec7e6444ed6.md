
# yy yy to Yank One Line

Just as d RETURN deletes two lines, y RETURN yanks two lines. Use the yy command to yank and dd delete the current line.

# D Works Differently From Y

The D command (page 434) does not work in the same manner as the Y command. Whereas D deletes to the end of the line, Y yanks the entire line, regardless of the cursor position.

# Copying Text from the Buffer

The Put commands, P and p, copy text from the General-Purpose buffer into the Work buffer. If you delete or yank characters or words into the General-Purpose buffer, P inserts them before the current character, and p inserts them after it. If you delete or yank lines, sentences, or paragraphs, P inserts the contents of the General-Purpose buffer before the line the cursor is, and p inserts them after.

Put commands do not destroy the contents of the General-Purpose buffer, so it is possible to place the same text at several points within the file using Delete or Yank command and several Put commands.

Because vim has only one General-Purpose buffer and vim changes the Change, Delete, or Yank command, you can use only cursor-movement commands between a Delete or Yank command and the General-responding Put command. Any other commands change the contents of the General-Purpose buffer and change the results of the Put command. If you do not plan to use the Put command immediately after a Delete or Yank, use a Named buffer rather than the General-Purpose buffer.

# Deleting Text Copies into the Buffer

Any of the Delete commands described earlier in this chapter (page 433) automatically place the deleted text in the General-Purpose buffer. Just as you use the Undo command to put the deleted text back where it came from, you can use a Put command to put the deleted text at another location in the Work buffer.

For example, if you delete a word from the middle of a sentence using the dw command and move the cursor to a SPACE between two words and give a p command, places the word you just deleted at the new location. If you delete a line by using the dd command and then move the cursor to the line below the line where you want the deleted line to appear and give a P command, places the line at the new location.

# Optional

# Named Buffers

You can use a Named buffer with any of the Delete, Yank, or Put commands. Each of the 26 Named buffers is named by a letter of the alphabet. Each Named buffer can store a different block of text so that you can recall each block as needed. Unlike the General-Purpose buffer, vim does not change the contents of a Named buffer unless you use a command that specifically overwrites it. The vim editor maintains the contents of the Named buffers throughout an editing session.

The vim editor stores text in a Named buffer if you precede a Delete or Yank command with a double quotation mark ("") and a buffer name (for example kky yanks a copy of the current line into buffer k). You can use Named buffer in two ways. If you give the name of the buffer as a lowercase letter, it overwrites the contents of the buffer when it deletes or yanks text into the buffer. If you use uppercase, vim appends the newly deleted or yanked text to the end of the buffer. This feature enables you to collect blocks of text from various sections of a file and then deposit them at one place in the file with a single command. Named buffers are also useful when you are moving a section of a file and do not want to use Put immediately after the corresponding Delete and when you want to insert a paragraph, sentence, or phrase repeatedly in a document.

If you have one sentence that you use throughout a document, you can yank the sentence into a Named buffer and put it wherever you need it using the following procedure. After entering the first occurrence of the sentence and pressing ESCAPE to return to Command mode, leave the cursor on the line containing the sentence. (The sentence must appear on a line or lines by itself for this process to work.) Then yank the sentence into Named buffer by giving it the "ay command (or "a2y" if the sentence takes up two lines). Now every time you need the sentence, you can return to Command mode and give the command "ap to put a copy of the sentence below the line the cursor is on.

This technique provides a quick and easy way to insert text that you use frequently in a document. For example, if you were editing a legal document, you might use a Named buffer to store the phrase The Plaintiff alleges that the defendant to save yourself the trouble of typing every time you want to use it. Similarly, if you were creating a letter that frequently used a long company name, such as National Standards Institute, you might put it into a Named buffer.

# Numbered Buffers

In addition to 26 Named buffers and 1 General-Purpose buffer, there are 9 Number buffers. These are, in one sense, readonly buffers. The vim editor automatically fills them with the nine most recently deleted chunks of text that are at least one line long. The most recently deleted pattern is held in "1, the most recent in "2", and so on. If you delete a block of text and then give other commands so you reclaim the deleted text with Undo, use "1p to paste the most recently deleted chunk of text below the location of the cursor. If you have deleted several blocks of text and want to reclaim a specific one, proceed as follows: Paste the contents of the buffer with "1p. If the first buffer does not have the text you are looking for, undo the paste with u, and then give the period (.) command to repeat the previous command. The Numbered buffers work in a unique way with the period command: instead of pasting the contents of buffer "1, the period command will paste the contents of the next buffer ("2.

# Reading and Writing Files

The vim editor changes the text in the buffer, but it does not change the file on disk. This section discusses other ways of reading and writing.

# Reading Files

The Read command reads a file into the buffer. It does not overwrite the file on disk, but it replaces the contents of the buffer with the contents of the file. You can specify which part of the file to read by using an address field. The format of the Read command is

```
:[address]r [filename]
```

As with other commands that begin with a colon, the filename the Read command displays is the one the Write command uses if you give a :w command (rather than :w filename). If you omit the filename, vim reads the file you are editing.

# Writing Files

The Write command writes part or all of the Work buffer to a file. You can use an address to write part of the Work buffer and a filename to specify a file. If you do not specify a filename, vim writes to the file you are editing. The formats of the Write command are

```
:[:address]w[!] [filename]
:w filename
```

You can use the second format of the Write command to append text to an existing file. The following list covers the components of the Write command.

- address: If you use an address, it specifies the portion of the Work buffer that you want to write to the disk. The address follows the form of the Substitute command. If you do not use an address, vim writes out the entire contents of the Work buffer.
- w: Because vim can quickly destroy a large amount of work, vim demands that you need an exclamation point following the w as a safeguard against accidentally writing a. The only times you do not need an exclamation point are when you are writing out the entire contents of the Work buffer to the file being edited (using no address and no filename) and when you are writing part of the buffer to a new file. When you are writing part of the file to the file being edited or when you are overwriting another file, you must use an exclamation point.
- filename: The optional filename is the pathname of the file you are writing to. If you do not specify a filename, vim writes to the file you are editing.

# Identifying the Current File

The File command provides the same information as the Status command (CONTROL-G); it displays the name of the file you are editing, whether the file has been modified and/or locked, the line number of the current line, the total number of lines in the Work buffer, and the percent of the Work buffer preceding the current line. The filename the File command displays is the one the Write command uses if you give a :w command (rather than :w filename). The File command is

```
:f
```

An example of the display produced by the File command is

```
"practice" [Modified] line 11 of 35 --31%--
```
