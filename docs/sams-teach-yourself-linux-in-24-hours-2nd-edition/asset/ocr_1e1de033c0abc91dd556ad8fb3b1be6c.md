```
mississippi
& mississippi 1 0: Mississippi

truncate
*
[Ctrl-d]
#
```

Notice that ispell starts, prints a short version message, and then waits for your input. When you enter a misspelled word, ispell echoes the word back and if a suggested replacement is found, prints the replacement with a number. Also note that ispell even corrects words spelled correctly but not properly capitalized. Finally, if you enter a correct word, ispell merely echoes back an asterisk. To quit, enter an end of text character by pressing Ctrl+D.

# Summary

This hour introduced you to a number of word processors, editors, and text utilities for OpenLinux. You now also know how to spellcheck text documents using the ispell command and how to quickly look up words from the command line.

# Q&A

Q I found that I made a lot of incorrect changes to a document when using xemacs. I know about the undo command, but is there are faster way to quickly fix things?

A The good news is the xemacs creates a backup file of your document. However, you can revert back to the original form of the document with the revert-buffer command. Press the Esc key, and then type the X key. At the command prompt (at the lower left of the xemacs window), type revert-buffer, and press Enter.

Q Help! I can't get printing to work with WordPerfect!

A Don't panic. See Hour 15, "Preparing Documents," for step-by-step directions on how to print with WordPerfect.

Q I entered a misspelled word into my personal dictionary when using ispell. How can I fix this?

A The personal dictionary is a simple text file. Open the file with your favorite text editor and remove or correct the word.