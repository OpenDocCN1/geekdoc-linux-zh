
## Tab Completion

Tab completion is an immensely helpful Emacs feature that ought to be one of the first time-saving techniques you learn. Any time you have to type something in the minibuffer, whether it is a file name, the name of a function or variable, or a Lisp library you'd like to load, tab completion will finish typing it for you.

If you have spent much time at a Linux shell prompt this will be a familiar concept. The common shells such as Bash use the tab key in a similar way to complete file and command names.

### File Name Completion

This type of completion is especially handy when you're running an operating system (such as Linux) that supports long file names. Here's how it works: If you type Ctrl-x Ctrl-f in order to load a new file and then type (in the minibuffer) the first few characters of the file name of a file you would like to load, pressing the Tab key notifies Emacs that you want it to finish typing the name.

Emacs checks the path. If it finds only one file name in the directory you specified that starts with the same letters, that name is completed in the minibuffer; pressing Enter loads the file. Otherwise, a message appears, telling you that the initial letters you typed aren't unique to one file. Pressing Tab a second time opens a Completions window that shows all the file names in the directory that begin with the characters you typed. Clicking the second mouse button on the file name you're looking for closes the Completions window and loads the file. If you move the cursor to the Completions window, you can also select the desired file name by moving point to the entry and pressing Enter.

### Help Key Completion

Help key completion works the same as the Ctrl-h help keys discussed previously. If you want help with a function whose name begins with "buffer", you press Ctrl-h f. The minibuffer becomes active and asks you to "Describe function:". Type buff and press the Tab key. (There is no reason to type more letters than the first few. In this case, it is reasonable to assume that most functions beginning with "buff" probably refer to buffers.) The first time you press the Tab key, "buff" is completed, and "buffer" is displayed in the minibuffer. Press the Tab key again, and the Completions window opens with a list of all Emacs functions beginning with the word "buffer." Again, clicking the second mouse button summons the documentation for any of the functions listed.

Sometimes it can be quicker to type the remainder of a name rather than press the Tab key a second time if you know the exact name you're looking for.

### Command Completion

Whenever you type an M-x command in the minibuffer, Tab completion saves you time. It's also a quick way to determine whether a command is available. If Emacs complains that there is "no match," either you mistyped the command, or there just aren't any available commands beginning with the letters you typed before pressing the Tab key.

### Moving around in a Buffer

Editing is no fun if moving from one area of a buffer to another is slow or awkward. Emacs has a variety of built-in commands for moving around the buffer, and with a little practice, they will become second nature to you.

#### By Characters, Words, and Lines

Like any other editor, Emacs lets you move the cursor around with the arrow keys. Because some keyboards lack the four arrow keys, these alternative keybindings are provided:

- Ctrl-f: Moves forward one character
- Ctrl-b: Moves backward one character
- Ctrl-right arrow: Moves forward one word
- Ctrl-left arrow: Moves backward one word
- Ctrl-p: Moves to the previous line
- Ctrl-n: Moves to the next line
- Ctrl-v: Moves to the next page (equivalent to Page Down)
- M-v: Moves to the previous page (equivalent to Page Up)

These keybindings are fine for moving the cursor short distances, but they can be tedious if you have a ways to go. The next section's keybindings address this.

#### By Sentences, Paragraphs, and Pages

Before using the following keybindings, you should be aware that Emacs has its own idea of just what sentences, paragraphs, and pages are. The definitions are somewhat arbitrary, but some standard had to be defined in order to have consistent editing behavior. Naturally, any or all of the definitions can be changed.

To Emacs, a sentence is a series of words terminated with a period and two spaces, unless it's at the end of a paragraph, when a period alone suffices.

A paragraph is defined as a block of text separated from other text with a blank line.

## Unprintable Characters

Emacs' idea of a page is different from that of a word processor. A word processor's page depends on the size of font being used and a document's formatting settings. Emacs is not a formatter; text in an Emacs file is like a continuous scroll with one portion visible in the editing window. The only reason you would need to define pages in a plain-text file would be if you were trying to accommodate a particular printer's page size.

Imagine you are using a printer that prints upon which 80 lines will fit, leaving room for header and footer blank areas. In typing a document to be printed on that printer, you can insert a control code every 80 lines in your file. This code is understood by most printers as a directive meaning “advance to the next page now.”

The only problem is that the control code isn't on your keyboard. Emacs provides a way to insert this sort of character by prefixing it with Ctl-q. Press Ctrl-q Ctrl-L in an Emacs text file, and what looks like ^L will appear on the screen. It's not really ^L, because ^L is two characters, ^ and L, whereas the result of pressing Ctrl-q Ctrl-L is one character, as you can see by moving the cursor over it with the arrow keys. The cursor will jump over ^L as if it were a single character, which it really is.

To sum up, Emacs considers the special control character ^L a page-break symbol. If you were to print a copy of a file that has ^L page breaks, they wouldn't show up in the printout, but new pages would begin whenever the character was encountered.

The following commands move point to a new location in the buffer:

- M-e Moves to the next sentence
- M-a Moves backward one sentence
- M-} Moves forward a paragraph
- M-{ Moves back to the previous paragraph
- Ctrl-x ] Moves to the next page
- Ctrl-x [ Moves to the previous page

## The Beginning and the End

How many times have you been typing near the end of a line and noticed a typo near the beginning? Being able to jump from the beginning to the very end of a file is handy as well.

- `Ctrl-a` Takes you to the beginning of the line
- `Ctrl-e` Puts the cursor at the end of the line
- `M-<` Moves point to the beginning of the file
- `M->` Moves point to the end of the file

I've always felt the latter two keybindings were awkward. In Chapter 10, you will learn how to assign new keybindings to common actions.

## Scrolling

Scrolling a window full of text sounds like something that shouldn't need adjusting. Unfortunately, Emacs has an odd way of scrolling that can be disconcerting to new users. The text tends to scroll smoothly for a short time and then abruptly jump several lines. Here is a situation in which the editor's configurability shines, allowing you to alter the default behavior in several different ways.

### Scrolling Variables

Several variables can be tweaked in order to adjust the scrolling to your satisfaction. If you prefer to scroll while preserving the relative point position on the screen, the variable `scroll-preserve-screen-position` can be set to a non-nil value. By default, the variable's value is nil; set it to 1 to activate this behavior.

`scroll-conservatively` is a variable that by default is set to 0. Try values such as 1, 2, or 3 to prevent point from jumping to the middle of the screen while you're scrolling. Two variables, `scroll-up-aggressively` and `scroll-down-aggressively`, offer further control of where on the screen point ends up when you're scrolling. The default value is 0.5, which tries to center point on the screen. Fractional values between 0 and 1 are valid.

The easiest way to try various values of these variables is via the Customize configuration facility, which is introduced in the next chapter. If you would like to try changing values now, you can evaluate the variable values in the \`Scratch' buffer by typing parenthesized statements that look something like this:

```
(setq scroll-conservatively 2)
```
