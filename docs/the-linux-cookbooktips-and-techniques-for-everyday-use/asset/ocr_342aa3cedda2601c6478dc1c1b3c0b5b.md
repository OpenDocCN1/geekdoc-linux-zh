![](bbox=[0.05, 0.07, 0.99, 0.46])

The large area with the word `beginning` in it is where the text is being streamed. The text in the lower-left window is a shrunken view of the entire file, the text in the lower-right window is the paragraph from which the current word comes from.

To open another file, choose it from the menu; you can have many files open in sview at once. sview places each file in its own buffer. You can also paste the X selection into a buffer of its own—to switch to a different buffer, choose its name from the Buffer menu.

Type Q to quit reading and exit sview.

The following table lists the keyboard commands used in sview and describes their meaning.

| KEYSTROKE | DESCRIPTION |
|---|---|
| @leftarrow | Decrease the stream speed. [GNU INFO BUG: any <> in the preceding line should be the <- arrow key.] |
| @rightarrow | Increase the stream speed. [GNU INFO BUG: any <> in the preceding line should be the -> arrow key.] |
| C-o | Open a file. |
| C-q | Quit viewing text and exit sview. |
| C-w | Erase the current text buffer. |
| M-n | Move forward to the next word. |
| M-p | Move backward to the previous word. |
| S | Toggle the streaming of text. |