
## Inserting Text

-   i—Inserts text to the left of the cursor
-   I—Inserts text at the beginning of the text in that line, not the beginning column of the vi screen
-   a—Appends to the right of the cursor
-   A—Appends at the end of the current line
-   o—Begins a new line below the current line
-   O—Drops the current line and begins a new one in its place

## Changing or Replacing Text

The following are incredibly useful when you're altering an existing file and need to change a character, a line, a sentence, or just a word:

-   cw—Changes a single word from the current cursor position. To change a whole word, you put the cursor on the first character of it.
-   c$—Changes the current line but doesn't extend to change the rest of a wrapped sentence on the screen.
-   r—Replaces the character under the cursor.
-   R—Replaces text on the same line until Esc is pressed, but it doesn't change text on the next line. Instead, it pushes it ahead of the current changes.

![](img/49f4f38f3aec011238fa50f89e643db3_108_0.png)

Remember to use the force multipliers in the appropriate places. You can easily change multiple words by using 5cw or replace 10 characters with 10r.

## Deleting Text and Lines

A more advanced use of vi is to remove or delete characters, words, or even lines. Be careful to check your deletions and changes, or press the u key to get things back to normal and try it again.

-   x—Deletes a single character under the cursor
-   X—Deletes a single character before the cursor
-   dw—Deletes a single word that's currently under the cursor, from the cursor position onward
-   dd—Deletes the current line entirely, regardless of the cursor position in the line
-   D—Deletes all text from the current cursor position to the end of the line
-   dL—Deletes all text from the cursor to the end of the screen
-   dG—Deletes all text from the cursor to the EOF
-   d^—Deletes all text from the beginning of the line to the cursor

> In the lexicon of computer software verbiage, *delete* in vi stores the cut or deleted string of text in the unnamed buffer for future use. This buffer's contents will be over-written by any further cuts or deletions.
>
> How you delete is important on the exam. If asked to delete from the current position to the end of the line, don’t pick or type the keys that delete the whole line— there are no partial credits on the exam!

## The Cut, Copy, and Paste Commands

The process of moving text around in vi is a little complex, so practice on a scratch file first. The following keystrokes are used to cut, copy, and paste text in a vi session:

-   yy—Copies a line of text to the unnamed buffer
-   3yy—Copies three lines of text to the unnamed buffer
-   yw—Copies a word (under the cursor) to the unnamed buffer
-   3yw—Copies three words to the unnamed buffer
-   p—Pastes the contents of the unnamed buffer to the right of the cursor
-   P—Pastes the contents of the unnamed buffer to the left of the cursor

Yanking (or copying) lines (the y key) and pasting (the p key) them back in are done on a whole-line basis, whereas yanking a word or several words is done solely on a word basis. Pasting data back in happens to the right of the current cursor position, so take care to put the cursor directly to the left of the desired insertion point. Pasting puts lines as a new entry directly below the current cursor line.

> **NOTE** A common use of the cut, copy, and paste commands is in the /etc/fstab file when you’ve added another file system or disk. Open the file, find a line similar to the desired new one, and press yy; then move the cursor to the line above the position you desire for the line, then press yy. The yanked line will appear under the current cursor line.

## Named and Unnamed Buffers

The vi editor has a total of 27 buffers: 26 named buffers (a–z) and 1 unnamed buffer that is overwritten by each new operation.

Unless you have specified a named buffer, all operations use the unnamed buffer, and two operations right after each other have the second operation overwrite the data from the first operation.

Named buffer operations are always preceded by the double quotation mark (`“`), which tells the machine that a named buffer operation is to follow.

When you perform named buffer operations, the buffers must be referred to in the command as either a lowercase or uppercase letter of the alphabet (which is part of the command, and not sent to the buffer):

-   Lowercase buffer letter—Overwrites the buffer
-   Uppercase buffer letter—Appends to buffer

For example, the following string, when entered in Command mode with the cursor in column 1, causes line 1 to copy the next four lines to the named buffer (a), overwriting any contents of that named buffer:

```text
"a3yy
```

The Message Line echoes the number of lines and the operation, such as `3 lines yanked`

The syntax for the editing commands remains the same; just remember to precede the operation with a double quotation mark, a lower- or uppercase character, and then whatever operation you want to perform with that named buffer.

Other examples include

-   “ayy”—Yanks a line to the named buffer (a), overwriting the current contents
-   "A3y"—Yanks three lines from the current cursor position and appends the lines to the `A` buffer
-   "ap"—Pastes the `a` buffer to the right of the cursor (the case of the buffer letter is meaningless in paste operations)

Performing single-line operations with named buffers usually doesn't echo anything to the Message Line, but anything involving more than one line of data echoes the number of lines affected. Word operations are usually not noted in the Message Line either.

## Searching in vi

Searching for text in Linux utilities typically follows a common convention. In the `less`, `more`, and `vi` commands, a forward slash followed by a search term/string searches forward in the file from the current cursor position or the top of the file, highlighting found strings. Initiating a backward search from the cursor position is done with a question mark followed by the string to search for, such as ?string.

Searches are performed only in Command mode, so remember to press the Esc key to get back there.

Finding the next occurrence (whether a forward or backward search) is usually accomplished by pressing the unshifted `N` key to search forward. You press `Shift+N` for a backward search.

## Searching and Replacing

Searching a document for a given string or character to replace it is commonly performed either in `vi` while editing a given file or by the `sed` command on a large set of data. Both `vi` and the `sed` command share a common search-and-replace syntax, with small differences that won't confuse you if you use both. Indeed, learning to search and replace in one will teach you how to use it in the other.

The search-and-replace syntax is as follows:

```
action/tofind/replacewith/modifier
```

For example, the following string in vi replaces just the first instance of the string bob in the current line with the string B0B:

```
:s/bob/B0B/
```

To replace all instances of the string bob with B0B in the current line, you would use this line:

```
:s/bob/B0B/g
```

The g stands for global or doing the action on every found instance of the string.

To replace all instances of bob with B0B in the entire file, no matter how many exist or how many changes are made to each line, you would use this:

```
:%s/bob/B0B/g
```

![](img/49f4f38f3aec011238fa50f89e643db3_112_0.png)

> It’s critical that you read the exam question and all its answers (except for a fill-in-the-blank) to see exactly what is being asked for. A percent symbol (%) in front of the search-and-replace string is the only way to cause vi to search the entire file, and not just the current line.

## Fuzzy Searches

Finding matches for fuzzy searches in vi is a good thing to know about. In a fuzzy search, you find something you only know a part of.

For example, if you wanted to find all the instances of the word The at the beginning of a line, you could use this search:

```
/^The
```

To find all the instances of the word kernel at the end of a line, you could use this search:

```
/kernel$
```

In some instances, you’ll need to find what’s called a metacharacter. For example, say you wanted to find the instances in a file of the asterisk (*) character because it stands for many characters. You could use something like this:

```
/\* character
```

Another example might be finding the text kernel, with the period being treated only as a period. Otherwise, you’d find kernels, kernel?, kernel!, and so on. To find just kernel, you’d use the following:

```
/kernel\. 
```
