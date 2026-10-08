# ## Adding Text in vi

Now that we know how to move around the cursor, let's do something with it. You need to first learn about cursor movement, because the commands for adding text take place relative to the position of the cursor. Table 8-3 summarizes some commands for adding text.

Table 8-3 Adding Text In vi

| Command | Insertion Action |
| :--- | :--- |
| a | Append new text after the cursor. |
| A | Append new text after the end of the current line. |
| i | Insert new text before the cursor. |
| I | Insert new text before the beginning of the current line. |
| o | Open a line below the current line and insert. |
| O | Open a line above the current line and insert. |
| :r file | Read *file* and insert after the current line. |
| :nr file | Read *file* and insert after line *n*. |
| escape | Get back to command mode. |
| ^v char | Ignore special meaning of *char* when inserting. This is for inserting special characters. |

Let's now look at some examples for adding text into **wisdom** in Figure 8-7.