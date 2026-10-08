The Table 6-1 summarizes the command and path completion used in the previous examples.

| Word or Command<br>(type escape before each) | Result |
| :-------------------------------------- | :------------------------- |
| wordescape=          | Displays a numbered list of file names beginning with word. |
| wordescape*          | Replaces word with all files matched. |
| wordescape\          | Replaces word with the first file name that starts with word. |
| command wordescape=  | Displays a numbered list of file names beginning with word. |
| command wordescape*  | Replaces word with all files matched. |
| command wordescape_  | Inserts the last word of the last command at the cursor position. |
| command wordescape_3 | Inserts the third word of the last command at the cursor position. |

# File Name Expansion

In your general activities working with ksh, you have to perform a lot of file-name-related work, including crafting shell scripts that deal with file names. An overview of file name expansion is useful to ensure that you're comfortable with this topic before you start writing shell scripts.

Table 6-2 lists some common filename expansion and pattern matching.

![](bbox=[0.88, 0.63, 0.96, 0.7])