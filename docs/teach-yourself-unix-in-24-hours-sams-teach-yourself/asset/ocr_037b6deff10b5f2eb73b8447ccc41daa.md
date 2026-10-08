# Task 13.4: Search and Replace in emacs

DESCRIPTION Because emacs retains the line of screen for its own system prompts, searching and replacing is easier than in vi. Moreover, the system prompts for the fields and asks, for each occurrence, whether to change it. On the other hand, command isn't a simple key press or two, but rather it is an example of a named emacs command. A named emacs command is one that requires you to use its name, such as query-replace, rather than a command key or two.

Searching for a pattern is done by pressing C-s, and searching backward is done with C-r (mnemonic forward or reverse search). To leave the search you've found you want, press Escape, and to cancel the search, returning to your starting point, use C-g.

You might find that pressing C-s does very strange things to your system. In fact, ^s and ^q are often used as flow control on a terminal, and by pressing C-s, you're actually telling the emulator to stop sending information until it is a C-q. Flow control is the protocol used by your computer and terminal to make sure that neither outpaces the other during data Transmission. If this happens to you, you need to turn off XON/XOFF flow control. Ask your system administrator for help.

![](bbox=[0.189, 0.3733, 0.258, 0.4933])

Search and replace is a whole new feature in emacs. To start a search and replace, use M-x-replace. emacs will prompt for what to do. Once a match is shown, you can type a variety of different commands to affect what happens; n makes the change; n leaves it as is but moves to the next match; Escape or q quits mode; and automatically replaces all further occurrences of the pattern without further prompting.

ACTION

+   1. I'm still looking at the dickens.note file, and I have moved the cursor to the top-left corner using M-<. Somewhere in the file is the word revolution, but I'm not sure where. Worse, every time I press C-s, the terminal freezes until I press C-q, because of flow control problems. Instead of searching forward, I'll search backward by first moving the cursor to the bottom of the file with M-> and then pressing C-.

```
----Emacs: dickens.note-----------(Fundamental)---Bot----
I-search backward:
```