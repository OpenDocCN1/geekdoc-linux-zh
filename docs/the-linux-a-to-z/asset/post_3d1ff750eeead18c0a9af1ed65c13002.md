
Putting a number before any of the commands in this block extends their function as follows:

- ns substitute next n characters with new text;
- ncw change n words to the right of the cursor;
- ncb change the n words before the current cursor;
- ncd change next n lines with new text.

In addition to the previous commands there are also two further change commands which can prove useful:

- c$ change characters to end of line for new text;
- c0 change characters to start of line for new text.

## 3.3 Command Mode

All the commands covered so far have been fairly simple, at least in terms of the number of keystrokes required to enter them. However, there are a large number of commands with a more complex structure, and also a lot of configuration options which can be set. All of these are entered via command mode. All the command mode features have one thing in common - they all start with a colon (:). As soon as you enter the colon, the cursor will jump to the start of the bottom line of the screen, where a colon will be displayed. Any characters you type now, up to a Return or Enter, will appear along the bottom line of the display so that you can check and, if necessary, correct your input.

### 3.3.1 Quit Commands

The only way you have seen to exit from the editor is to use the ZZ command in edit mode. This not only exits but also saves any changes you have made to your text back into the original file, overwriting its previous contents. It may be that you only want to exit from the editor without saving the editor contents. This can be because you have made no changes to the text or because, having changed the text, you now wish to abort the changes and quit the editor anyway. The two commands to do this are:

- :q quit the editor if no changes have been made;
- :q! quit the editor aborting any changes made.

It is good practice to get into the habit of using :q where you can as this will reduce the chance of typing :q! by accident, which might result in the loss of some valuable material.

### 3.3.2 File Manipulation

The next set of colon commands to look at allow you to write and read blocks of text to and from files:

- `:w` write editor contents to original file;
- `:wq` write file and quit editor (same as ZZ);
- `:w file` write editor contents to named file;
- `:r file` read file into editor after cursor line;
- `:e file` edit a new file replacing old contents;
- `:f file` change the name of the current text to file;
- `:f` print the name and status of the current text.

The :w command writes the text you are editing back to the file whose name you specified when you first entered vi. This command doesn't exit from the editor but leaves you in edit mode after the file write takes place. This is a command you should use from time to time to save any changes you have made so far. The :wq command just combines the effect of :w followed by :q.

Sometimes you may want to modify the contents of a file, but then write the changed version back to a new file, leaving the original file unchanged. This is done with :w file. Another variation on this command allows you to specify a comma-separated range of line numbers before it. This just writes the appropriately numbered lines to the specified file:

```
:a,bw file  write lines a to b inclusive into file
```

The :r command is used to insert the contents of a specified file into the current text after the current cursor line. This can be useful for building new files up from previously prepared pieces.

When you finish with the current text, if you want to edit another file without having to exit vi and re-enter it, you use the :e file command. At any time during the editing of a file you can change the name that vi will use for the file by default. This is done with the :f file command. If you omit the file name after this command then vi will list the current name it is using for the text along with some status information including the number of lines in the text and the line number of the current cursor line.

### 3.3.3 Line Numbers

All the lines in the text being edited have a line number associated with them. You can move the cursor directly to a particular line with the command:

```
:n  move cursor to line n
```

where n is the number of the line to which you wish to move.

It is possible to have vi add line numbers to the text displayed and this is covered later in Section 3.3.8.

Wherever it makes sense, the colon commands can have a range of line numbers specified upon which the command will then operate. There are several different ways in which the line numbers may be given. First, you may specify numeric values, which are treated just as absolute line numbers. A period (or full stop ‘.’) given as a line number refers to the current cursor line, whatever line number it happens to be. And a dollar sign ($) refers to the last line in the file. You can also specify simple numeric expressions for line numbers like .+5, which means five lines on from the current cursor line. Some example commands using these ideas are:

| Command | Description |
|---|---|
| `:345` | move the cursor to line 345; |
| `:345w myfile` | writes line 345 out to myfile; |
| `:3,8w myfile` | writes lines 3 to 8 inclusive out to myfile; |
| `:1,.w myfile` | write from line 1 to the current cursor line; |
| `:.,$w myfile` | write from current cursor line to end of file; |
| `:.,+4w myfile` | write five lines from current cursor line; |
| `:1,$w myfile` | write whole file (same as :w myfile). |

### 3.3.4 String Searching

In addition to specifying lines by number, you can also specify lines by giving a text string to search for, on those lines. The text strings to search for are enclosed between slash (/) characters if you want to search forwards through the text from the current position, or question mark (query ‘?’) characters if you want to search backwards through the text:

| Command | Description |
|---|---|
| `:/str/` | move cursor on to next line containing str, |
| `:?str?` | move cursor back to next line containing str, |
| `:/str/w myfile` | write to myfile first line containing str; |
| `:/str1/,/str2/w myfile` | write lines from str1 to str2. |

### 3.3.5 Regular Expressions

When you specify a search string to vi, there are several characters that can be included which have special meanings. Search strings which include these special characters are known as regular expressions.

For example, suppose you wanted to search for a line of text which contained the word struct at the start of the line. The command:

```
:/struct/
```

would not do, because this would find the first line containing the word struct in any position on the line, not just at the beginning. The solution here is to use the ^ (caret) special character at the start of the search string:

```
:/^struct/
```

The ^ character matches the start of the line, so the previous command means: find a line which has the start of the line followed by the string struct.

Similarly, you can find words at the end of a line by using the end of line special character ($) at the end of the search string:

```
:/struct$/
```

The following table gives a list of most of the special character sequences and their meanings:

| Sequence | Meaning |
|---|---|
| `^` | at the start of string, matches start of line; |
| `$` | at the end of string, matches end of line; |
| `\<` | matches the start of a word; |
| `\>` | matches the end of a word; |
| `.` | matches any single text character; |
| `[str]` | matches any single character in str; |
| `[^str]` | matches any single character not in str; |
| `[a-b]` | matches any character between a and b; |
| `*` | matches zero or more repeats of the previous character; |
| `\` | turns off any special meaning of the character following. |

### 3.3.6 Text Substitution

The :s command is used to substitute one string of characters on a line for another. In fact, there are several variations on this command. These can substitute the first occurrence of a particular string on a line with a new string, or substitute every occurrence of the string on a line, or substitute all occurrences of the string in a block of lines or even the whole file:

```
:s/str1/str2/      substitute first str1 on this line by str2;
:s/str1/str2/g     substitute every str1 on this line by str2;
:.,$/str1/str2/g   substitute every str1 to end of file by str2;
:1,$/str1/str2/g   substitute every str1 in whole file by str2;
:g/str1/s//str2/g  another way to substitute every str1 by str2.
```

In these substitution commands, a g at the end of the command specifies that the command is to be repeated for each occurrence of the search string on the current cursor line. Without the g, the command only operates on the first occurrence of the search string on the line. The g at the start of the command specifies that the command is to be performed for each line in the file which contains the search string.
