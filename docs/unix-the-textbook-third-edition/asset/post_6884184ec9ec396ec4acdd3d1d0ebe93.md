
## TABLE 3.14 Interactive Search and Replace

| Search and Replace Action | Keystrokes |
|---|---|
| Search forward | <Ctrl+S> |
| Search backward | <Ctrl+R> |
| Regular expression search | <Ctrl+Alt+S> |
| Reverse regular expression search | <Ctrl+Alt+R> |
| Select previous search string | <Alt+P> |
| Select next later search string | <Alt+N> |
| Exit incremental search | <Enter> |
| Undo effect of last character | <Del> |
| Abort current search | <Ctrl+G> |
| Interactively replace a text string | <Alt+%> |
| Using regular expressions | <Alt+X> query-replace-regexp |
| Replace this one, go on to next | <Space> or y |
| Replace this one, don't move | , |
| Skip to next without replacing | <Del> or n |
| Replace all remaining matches | ! |
| Back up to the previous match | ^ |
| Exit query-replace | <Enter> |
| Enter recursive edit (<Ctrl+Alt+C> to exit) | <Ctrl+R> |

![](img/02e070097d401d3bf7de4bf1c470b267_148_0.png)

## FIGURE 3.9 Display after Step 21.

### 3.3.6.1 Practice Session 3.10

Step 1: At the shell prompt, type emacs osfile and then press <Enter>.

Step 2: Type Windows is the operating system of choice for everyone.

Step 3: Press <Ctrl+@>. The mark is now set at the end of the line you typed in Step 2. Highlight the whole first line with the graphics cursor and left mouse button. This will define the region that will be put in the Kill Ring.

Step 4: Press <Esc+W>. This action copies the region to the Kill Ring.

Step 5: Press <Enter> to start a new line in the buffer, which should be blank. The cursor should be positioned at the start of this new line.

Step 6: Press <Ctrl+Y>. The first line of text is now pasted into the next blank line from the Kill Ring.

Step 7: Repeat Steps 5 and 6 six more times so that you now have eight lines of text in the buffer, all containing the text Windows is the operating system of choice for everyone.

Step 8: Position the cursor on the W in Windows on the first line of the buffer.

Step 9: Save the buffer at this point with <Ctrl+X> <Ctrl+S>.

Step 10: Press <Esc+X>. Then type query-replace and press <Enter>. These actions begin an interactive search and replace. The prompt Query replace: appears.

Step 11: Type everyone and then press <Enter>. The prompt with: appears.

Step 12: Type students and then press <Enter>. The prompt Query replacing everyone with students: (? for help) appears.

Step 13: Pressing <Space> on the keyboard replaces the word everyone on the first line with the word students, and the prompt Query replacing everyone with students: (? for help) appears again.

Step 14: Press <Enter>. The prompt Replaced 1 occurrence appears.

Step 15: Position the cursor over the e in the word everyone on the second line of the buffer.

Step 16: Repeat Steps 10–14, interactively replacing the word everyone each time it appears with the words computer scientists, engineers, system administrators, web servers, scientists, networking, and mathematicians on lines 2–8 of the buffer.

Be sure that the second through eighth times you do Step 16, you always position the cursor on the previous line to the current line you want to replace text on!

Step 17: Position the cursor on the W in Windows on the first line of the buffer.

Step 18: Press <Esc+X>. Then type replace-string and press <Enter>. These actions begin an unconditional search and replace. The prompt replace string: appears.

Step 19: Type Windows and then press <Enter>. The prompt Replace string Windows with: appears.

Step 20: Type UNIX and then press <Enter>. The prompt Replaced 8 occurrences appears. Correct?

Step 21: Save the buffer with <Ctrl+X><Ctrl+S>, print it using the facilities available on your computer system, and exit emacs with <Ctrl+X> <Ctrl+C>. Your screen display should appear like Figure 3.9.

The following in-chapter exercises ask you to apply some of the operations you learned about in the previous practice sessions:

## EXERCISE 3.8

Run emacs and define keyboard macro commands that automatically delete

- a. every other word in a line of unspecified length,
- b. every other line in a file of unspecified length,
- c. every other word and every other line in a file of unspecified length with lines of unspecified length.

## EXERCISE 3.9

Write a keyboard macro, as shown in Section 3.3.5, to do everything shown in Steps 10–14 of Practice Session 3.10.

To get some further practice with emacs, do Problem 16 at the end of the chapter.

## 3.3.7 How to Do Purely Graphical Editing with GNU Emacs

Up to this point in our work, it was possible to use emacs in a single text-based terminal window and obtain the results shown. If you connect to UNIX by using one of the methods described in Chapter 2 you are likely interfacing with the operating system via an intermediary known as the X Window System, which would allow you to do all of your emacs work in a graphical environment. We present more information on the X Window System and some of its facilities (e.g., the particular features of the GUI) in Chapter 22. For the purposes of learning emacs—if you are using UNIX and the X Window System—you may be able to run emacs in its own frame on your screen display or possibly in several frames on your screen display simultaneously. Be aware that in our base UNIX systems, PC-BSD and Solaris, the latest version of GNU graphical emacs version is available through the package management facilities in those systems, as described in Chapter 23.

## 3.3.8 Editing Data Files

The following practice session demonstrates the use of graphical GNU emacs to do some further editing of the datafile created in Practice Session 3.9. The look and feel of GNU emacs, running under the X Window System using the KDE or Gnome desktop default windowing environments in PC-BSD and Solaris, is very similar to a word processor or desktop publishing application running under any other operating system that has a GUI, such as Windows 10 or Mac OS X. In the practice sessions that follow, we are using GNU emacs 24.3.1.

### 3.3.8.1 Practice Session 3.11

Step 1: In a terminal or console window, at the shell prompt, type emacs datafile and then press <Enter>. Your screen display should look similar to the one shown in Figure 3.8.
