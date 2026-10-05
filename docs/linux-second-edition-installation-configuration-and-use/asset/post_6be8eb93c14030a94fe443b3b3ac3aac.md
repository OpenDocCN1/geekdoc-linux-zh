
# EMACS - KING OF ALL EDITORS

## Rectangle commands

| Ctrl+Spacebar | set marking point |
| Ctrl+X, R, O | open rectangular area (rectangle option), that is, fill the rectangular area with spaces |
| Ctrl+X, R, K | delete the rectangular area (rectangle kill) |
| Ctrl+X, R, Y | insert the deleted rectangular area at the current cursor position (rectangle yank) |
| Alt+X string-rectangle | insert text before each line of the marked area |

Besides this, Emacs has some further processing modes in which indenting is carried out. In C mode, for example, program lines are indented or outdented by spaces at each curly bracket (brace, { or }) (see page 558).

## # 16.7 Flow text

Up to now we have assumed that you use Emacs to process texts in which each line constitutes a unit (for example, program listings, configuration files, and so on). Things look slightly different when you want to use Emacs to process flow text. Here the unit is a paragraph (of one or more lines). When inputting lines, the text automatically 'flows' into a new line.

Normally, Emacs does not carry out line breaking. When lines are longer than the screen or window width, a \ character is inserted at the left end and the text is continued in the next line.

If you want to break a single line, you can execute the Alt+Q (in all processing modes); this replaces space with breaks at the appropriate points. Thus, a long line is turned into several short lines. Please note, however, that Emacs considers all lines which are not separated from other lines by a completely empty line as a single paragraph. Emacs reformats the whole paragraph (that is, all lines which belong together). In a program listing, the consequences of this command are obviously fatal! Use Ctrl+X, U to undo it.

When you process TeX or LaTeX, features that begin with a \ character are considered a paragraph boundary and are not reformated. In order to carry out line breaking, you must first join the line manually with the previous line and re-execute Alt+Q.

When entering new text, the repeated execution of Alt+Q becomes irritating. Therefore, a special flow text mode is provided which is activated with Alt+X auto-fill-mode. When Emacs is in this mode, every newly entered text is automatically broken up. Already existing text is not changed by this mode. Also, deleting text does not lead to automatic reformatting, which is why line breaking must often be forced manually by changes in already existing flow text.

## FLOW TEXT 553

Lines are normally broken after a maximum of 70 characters. You can, however, modify the column where you want lines to be broken with the following command: `Alt+X` set-variable `fill-column n`. Obviously, you can also specify a corresponding setting in `.emacs` (see page 584).

## Indent line breaking in flow text

- `Alt+Q` carries out manual line breaking
- `Alt+X` activates auto flow text mode (automatic line breaking)

## Indenting flow text

When you want to enter several paragraphs of indented text, you can prevent the first valid column. To do this, you must enter many spaces or tabs in an otherwise empty line as your text is to indent. Subsequently, you execute `Ctrl+X` (that is, `Ctrl+X`, full stop). Now, Emacs indents all lines from the second line of a paragraph toward the specified indent column.

The indenting column only applies to newly entered text. Indenting existing text must be done with the method described above, with no (!) indenting column defined. Therefore, you must deactivate your indenting column by placing the cursor at the beginning of a line and re-executing `Ctrl+X`.

> `Ctrl+X` command actually stores the characters between the current cursor position and the beginning of the line and automatically inserts them at the beginning of each new line break. If you execute `Ctrl+X` while the characters left of the cursor position contain text, this is inserted at the beginning of each new line. This can be used to write several lines that start with a given character string (for example, >).

For reformatting amounts of text that are indented in various ways, Emacs provides the command `Alt+X` fill-individual-paragraphs. This command formats the area between the marking point (`Ctrl+Space`) and the current cursor position. All current indents are maintained.

## Indenting flow text

- `Ctrl+X` defines the indent column by means of the current cursor position; for this, the cursor must be in an empty line
- `Alt+M` moves the cursor to the beginning of an indented line (similar to `Ctrl+A`)
- `Ctrl+Spacebar` sets the marking point
- `Alt+X` fill-individual reformats the area between the marking point and the cursor position, maintaining the current indents

## Text mode

If you work with indents, the indented text mode be more convenient than the above procedures: this mode is activated with Alt+X text-mode. When you want to process flow text in this mode (which will normally be the case), you must also activate the appropriate minor mode with Alt+X auto-fill-mode. Minor modes define some additional commands which can be used in parallel with an arbitrary major mode – see also page 558.)

The only essential feature of the indented text mode is that, when breaking lines, Emacs automatically and without complicated preparations each new line by the same amount as the preceding one. Also, Alt+Q for manual line breaking now follows the first line indent without 'ifs' or 'bits'.

In addition, the indented text mode has two new commands: Alt+S centers the current line.

| Command | Description |
| :--- | :--- |
| Alt+X text-mode | activates text mode |
| Alt+X auto-fill-mode | activates auto-fill mode |
| Alt+Q | carries out line breaking |
| Shift+S | centers the current line |
| Shift+S | centers the paragraph |

If you want to center lines or paragraphs without switching to text mode, you can call the corresponding commands with Alt+X, respectively.

## 16.8 Searching and replacing

### Incremental search

The quickest way to search for text is to use Ctrl+S. Compared with the search in other editors, this command has a special feature: it starts as soon as the first character of the search has text. If, for example, you search for 'second mode' and enter Ctrl+S, the cursor jumps to the first word that starts with 'sec'. (If you only enter case, Emacs does not differentiate between upper and lower case.)

If at this point you were actually looking for 'sending mode', delete the 'c' and Emacs jumps back to the first word (starting with search began) that begins with 'se'. If you now enter 'n', Emacs advances to the first word that starts with 'sen'. Just try it out!

As soon as you press ← or a cursor key, Emacs assumes the search is finished and places the cursor at the found position. The beginning of the search is stored as a marking point. Therefore you can easily move the cursor to where it was before the search was started – by simply entering Ctrl+S. A repeated execution of Ctrl+X, Ctrl+X gets you back to the position of the search text.

By pressing Ctrl+S twice, you can resume the search and jump to the next occurrence of the search text. If you want to search backwards, just press Ctrl+R instead of Ctrl+S.

## Incremental search

- Ctrl+S incremental search forward
- Ctrl+R incremental search backward
- Alt+P selects a previously used search text (previous)
- Alt+N selects a previously used search text (next)
- Ctrl+G aborts the search
- Ctrl+X, Ctrl+X exchanges marking point (start of search) and current cursor position

If at a later time you want to search for text which you have searched earlier, you can select a text from the stored list of search texts with Ctrl+S followed by Alt+P (previous) and Alt+N (next).

## Pattern search (with regular expressions)

Incremental search finds text which exactly corresponds to the search text. Often, however, it is desirable to search for texts that match a given pattern.

## Search for regular expressions

- Ctrl+Alt+S incremental pattern search forward
- Ctrl+Alt+R incremental pattern search backward

Structure of the search pattern

- \< beginning of a word
- \> end of a word
- ^ beginning of a line
- $ end of a line
- . an arbitrary character with the exception of the line feed character
- .* an arbitrary number (including 0) of arbitrary characters (like * in file names)
- .+ an arbitrary number of arbitrary characters (but at least one)
