
The text that you're searching for goes in the Text to find edit field in the dialog box. You then tab down to the two options fields. These are check boxes, and they both default to blank. The first specifies a case-sensitive search. If you check it, the text found must match the text you enter in Text to find both in characters and case.

The second check box specifies that the search must be for Whole words only. This allows you to avoid finding strings inside of larger strings. For example: Suppose you're looking for the register name “AX.” In the middle of your assembly file, you have a comment that reads like this:

+   : Axe the dead space at the end of the string

If you don't check Whole words only, your search for “AX” will also find “Axe” because “ax” is inside “axe.” You could also discriminate between the two by case, but that's less reliable, especially when you're searching source code files written by other people who may have entirely different habits using character case. (Or who aren't consistent in how they use it—even worse.)

If Words is only checked, a search for “AX” will not find “Axe,” or “Tax,” or “maximum,” or anything else that isn't simply ... “AX.”

Once you have the Find dialog box filled the way you want it, press the OK button. The search will commence, and if the search is successful the cursor will move to the first character of the first instance of the found text string. If the editor cannot find any instance of the requested text string in the work file, it displays an error box containing the message “Search not found.” You must then click on the OK button to continue editing.

## Searching for Additional Instances

Most assembly language source code files will have multiple instances of common identifiers like “AX.” If you want to find not the first one but the third or fourth (or one further down that you know you can identify from its context), you need to search for additional instances of the text. NASM-IDE has a command for this: Search again. This command may be issued from the menu bar, by selecting menu item Search Search again. The shortcut for Search again is Ctrl-L, which is very handy. (Sometimes using the mouse is more hand motion than it needs to be.)

## Ctrl-L will find (or replace) the next instance of a given text string

## Replacing Found Text

Many times, the whole reason for finding a text string is to replace it with something else—sometimes simply once but for every instance of the text string in the file. NASM-IDE has special machinery to do exactly this: the Replace command. Once the search text is found, NASM-IDE will replace the search text with replacement text that you provide.

As with Find, you can issue the Replace command either from the menu bar by selecting the Search | Replace menu item, or from the keyboard by pressing Ctrl-QA.

Ctrl-QA will find and replace a given text string with your text.

As with Find, the Replace command brings up a dialog box, (shown in Figure 5.8) which you must enter:

- 1. The text you're searching for.
- 2. The text you want to replace the found text.
- 3. The kind of search you want to conduct (that is, whole words only or case-sensitive or both).
- 4. Whether to prompt for each replacement.
- 5. Whether to sweep through the file and replace all instances of the original text with your replacement text.

The search options are the same as I described for the Find command. If you leave the Replace dialog box in its default state and click OK, the editor will locate the first instance of the search string, highlight it, and display another dialog that asks the question: “Replace this instance?” You can click on the Yes button to replace the instance, the No button to leave it alone, or the Cancel button to end the Replace operation. (Cancel is most useful when you're doing a Replace all operation and running through the whole file replacing every instance of some text string.)

Note that just as with the Find command, you can use the Ctrl-L hot key to perform a subsequent Replace command on the next instance of the text string you just replaced. Each Ctrl-L will locate and replace the next instance of the search text until no more instances of the search text are found in the file.

## ASSEMBLY LANGUAGE STEP-BY-STEP

![](img/5af1f694a521bb214c2fd03b770b346f_175)

## Saving Your Work

It's very important to remember what to save while you edit. By default, NASM-IDE shows 25 lines, but you can change this in the Options | Environment menu. The dialog box shown in Figure 5.9 will appear. The top pane governs the screen size. The default is 25, but you can check 43/50 instead by clicking on. Then when you click on OK, the screen size will change immediately. What it changes to depends on your hardware. If you have an EGA (Enhanced Graphics Adapter) (which is most unlikely in the year 2000), you'll get 43-line screen. If you have a VGA (Video Graphics Array) or anything more recent than the VGA, you'll get a 50-line screen. Note that these are mutually exclusive; a single system (as far as I know) let you choose from 43 lines or 50 lines.

## Changing the Display Size

By default, NASM-IDE shows 25 lines, but you can change this in the Options | Environment menu. The dialog box shown in Figure 5.9 will appear. The top pane governs the screen size. The default is 25, but you can check 43/50 instead by clicking on. Then when you click on OK, the screen size will change immediately. What it changes to depends on your hardware.

## ASSEMBLY LANGUAGE STEP-BY-STEP

![](img/5af1f694a521bb214c2fd03b770b346f_177)

Figure 5.9 The Environment Options box.

## Exiting NASM-IDE

The easiest way to get out of NASM-IDE is the File | Exit item. The shortcut for Exit is Alt-F4, which is common. If you attempt to exit, NASM-IDE will bring up a dialog asking if you want to save. You can click on the Yes button to save, the No button to leave without saving, or the NASM-IDE will tuck itself away and open up a DOS shell. When you're done, you simply type "exit" and press Enter and in a pop you're back inside NASM-IDE as though you'd never left.

## DOS Shell

People who have grown up using nothing but Microsoft Windows have a little troublesome understanding what a DOS shell is or why it's useful. The answer, of course, is that there was a time when we didn't have Windows and couldn't just click on a window and open up another program without closing the first.

A DOS shell was a very handy thing to have in the DOS era, and NASM-IDE provides one. If you select the File | DOS menu item, NASM-IDE will tuck itself away and open up a DOS shell. It's like exiting NASM-IDE without really exiting it. You can run DOS programs, look at and copy files, and so on. When you're done, you simply type "exit" and press Enter and in a pop you're back inside NASM-IDE as though you'd never left.
