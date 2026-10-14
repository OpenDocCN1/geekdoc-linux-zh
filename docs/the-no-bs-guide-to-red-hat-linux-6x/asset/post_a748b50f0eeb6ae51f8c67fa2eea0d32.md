
## CHANGING TEXT AND MOVING THROUGH YOUR DOCUMENT

To change text that's already in the file, you first need to reach it. You can move through your file in various ways. The arrow keys provide the simplest way, and they work just like you'd expect them to—they move you character by character through your file.

If you want to jump to the beginning or end of the current line, use the HOME and END keys, respectively. You can jump from word to word using ESC-F and ESC-B, or you can scroll page by page using CTRL-V (next page) and ESC-V (previous page). On some keyboards, the PGUP and PGDN keys work, too.

Text that you enter is inserted to the left of the cursor, and any text to the right of cursor is pushed to the right as you type. You can use the DEL key (or CTRL-D) to delete one character at a time, or press CTRL-K to delete all characters from the cursor to the end of the line.

## SEARCHING FOR TEXT

When you're working in a big file, you'll often want to locate a certain string of text. You can either scroll through the file until your eye catches it, or you can use CTRL-S to search using Emacs' less-than-elegant search tool.

As soon as you press CTRL-S, you can start to enter the text you want to find, but don't type too fast! As you enter your search string, Emacs immediately moves the cursor to a word in the file that matches what you've entered so far, so if you type too fast, you may miss something.

Try it. Starting at the top of the file, press CTRL-S and then type the letter b. The cursor should jump to the word bathtub right away. If you now type an r after the b, Emacs searches for br, and the cursor should jump to the word brightly. You can search backward, too, by using CTRL-R instead of CTRL-S.

## ADDING AND DELETING LINES

Let's practice adding and deleting lines now. To add a new line to your file, move the cursor to the end of a line (press END or use the right-arrow key), then press ENTER. A new blank line should appear after the current line. Pressing ENTER with the cursor at the beginning or end of a line adds a new blank line before the current line; pressing ENTER with the cursor anywhere else on a line splits the line at that point.

To delete a line, move to the beginning of the line (with the HOME key) and press CTRL-K. The line will become blank, but it will not go away. To delete the blank line from the file, press CTRL-K again or press the DEL key.

## CUTTING AND PASTING WITH EMACS

If you ever want to move a block of text from one spot in your file to another, you can use CTRL-K (kill) along with CTRL-Y (yank) to get the job done. When you press CTRL-Y, the last thing you “killed” with CTRL-K will be yanked back into the file. So to move a block of text, just kill one or more lines with CTRL-K, then put your cursor at the spot where you'd like to place the text and press CTRL-Y to yank it back.

For example, here's how to move the first line of the bulb.joke file to the end. With your cursor on the first character of the first line, press CTRL-K twice. (Line 1 disappears.) Press the down arrow twice to move your cursor to the third line of the file, which is now blank. Press CTRL-Y once to paste the deleted line at line 3 and then press CTRL-Y again.

You should now have two copies of the deleted line at the end of your file, which should look like Figure 7-5.

```
A: Two--one to hold the giraffe, and the other to fill the
bath tub with brightly colored machine tools.
Q: How many surrealists does it take to change a light bulb?
Q: How many surrealists does it take to change a light bulb?

--**Emacs: bulb.joke    (Fundamental)--All----------------
```

Figure 7-5: Entering text with Emacs

## QUITTING WITHOUT SAVING YOUR CHANGES

To leave Emacs without saving your changes, press CTRL-X and then CTRL-C. A prompt like this will appear at the bottom of the screen:

```
Save file bulb.joke (y, n, !, ., q, C-r or C-h)
```

Press n and then answer yes when Emacs asks:

```
Modified buffers exist; exit anyway? (yes or no)
```

Your Linux prompt will return, and the bulb.joke file will be just as it was before you started editing.

## PARTING WORDS ABOUT EMACS

We haven't even scratched the surface of what you can do with the Emacs editor. As its name suggests, you can write your own macros to add functionality to the editor or to automate repetitive editing tasks.

Take the time to go through the Emacs tutorial (accessed by pressing CTRL-H T) to get an idea of all the things you can do with it. Although it's not easy to learn all the various CTRL and ESC commands, if you're a programmer (or even if you dabble), Emacs' customizability makes it your best bet as a text editor.

The Usenet newsgroup comp.emacs is a good place to discuss Emacs or ask questions. You can find the Emacs FAQ file online at ftp://rtfm.mit.edu/pub/usenet/comp.emacs.

## THE PICO EDITOR

Pico, short for Pine Composer, started life as the built-in editor for the Pine email program. Lots of people use Pico as a text editor because they also use the friendly Pine program for email.

The Pico text editor doesn't have a lot of fancy features, but it's a welcome alternative to the vi or Emacs editors because learning it is quick and easy. Cursor movement and text entry are straightforward, and—best of all—you don't have to learn any arcane commands: all commands are listed in a handy menu at the bottom of the screen.
