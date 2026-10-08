# ## Deleting Text in vi

We also need to learn about cursor movement before learning how to delete text, because the commands for deleting text take place relative to the position of the cursor. Table 8-4 summarizes some commands for deleting text.

**Table 8-4 Deleting Text In vi**

| Command | Deletion Action |
| :------ | :-------------- |
| x       | Delete the character at the cursor. You can also put a number in front of x to specify the number of characters to delete. |
| nx      | Delete $n$ characters beginning with the current. |
| X       | Delete the previous character. You can also put a number in front of X to specify the number of previous characters to delete. |
| nX      | Delete previous $n$ characters. |
| dw      | Delete to the beginning of the next word. |
| ndw     | Delete the next $n$ words beginning with the current. |
| dG      | Delete lines to the end of the file. |
| dd      | Delete the entire line. |
| ndd     | Delete $n$ lines beginning with the current. |
| db      | Delete the previous word. |
| ndb     | Delete the previous $n$ words beginning with the current. |
| :n,md   | Deletes lines $n$ through $m$. |