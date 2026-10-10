+   red (l) - text editor
+   rlview (l) - Vi Improved, a programmers text editor
+   rlvim (l) - Vi Improved, a programmers text editor
+   textedit (lx) - Xlview window- and mouse-based text editor
+   vi (l) - Vi Improved, a programmers text editor
+   view (l) - Vi Improved, a programmers text editor
+   vim (l) - Vi Improved, a programmers text editor
+   xedit (lx) - simple text editor for X
+   xvi (l) - multi-file text editor

Note that not all the output is shown here (other types of text editing commands have been deleted). You will find many others installed on your system, including several for the K Desktop Environment. Each editor has its own set of particular strengths, weaknesses, and features.

While you may typically think of an editor as an interactive program with a moving cursor and the ability to visually insert, remove, or readjust words, lines, and paragraphs on the screen, Linux also comes with editors that work from the command line or through shell scripts. Editors with this ability, such as *sed*, are known as *stream* editors, and work on text from the standard input, then send the modified text on through the standard output.

If you have a document such as *myfile.txt*, but find that a person's name has been misspelled throughout, you can use *sed* to quickly edit and replace all occurrences with a single command line. For example, if the original text looks like this:

> Mr. Ho Lee Fook, one of the largest campaign raisers for Arlington County's recent Board of Supervisors election, and a long-time resident of Lyons Village, had recently been arraigned on charges of burglary in connection with a series of break-ins in various townhouse communities in Fairfax, Va. Fook, 39, was arrested Saturday as he was leaving RT's restaurant in the Courthouse section of Arlington, Va.

You can correct the error by using *sed*'s search operator, a forward slash (/) delimiter, which is followed by the text to find, another delimiter, the text to replace, and finally the globally replace operator. The command should appear like this:

```
$ sed s/Fook/O'Brien/g myfile.txt
```

> Mr. Ho Lee O'Brien, one of the largest campaign raisers for Arlington County's recent Board of Supervisors election, and a long-time resident of Lyons Village, had recently been arraigned