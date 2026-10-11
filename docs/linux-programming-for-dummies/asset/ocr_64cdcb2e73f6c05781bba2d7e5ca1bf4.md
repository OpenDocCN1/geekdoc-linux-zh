![](bbox=[0.14, 0.14, 0.92, 0.44])

Table B-5 contains the commands that you need to instruct *vi* to conduct a search of your text or program.

> Note: Words that appear in *italics* in the commands in this table you must replace with the characters or words that you’re trying to locate in your text.

| B-5<br>Command | What It Does |
| :--- | :--- |
| */ pattern* | Begins the search from the cursor position for the characters that compose the pattern you’re searching for. |
| */pattern/+n* | Places the cursor on the *n*th line after the line that contains the characters or words that you’re searching for. (Replace *n* with the number of the line.) Typing */Bob/+3*, for example, places the cursor on the third line below the line where *vi* finds the word *Bob*. |
| *?pattern* | Begins the search at the cursor and continues to search backward through the text. |
| *?pattern/~n* | Places the cursor on the *n*th line before the line that contains the characters or words that you’re searching for. Typing *?Bob?~3*, for example, places the cursor on the third line above the line where *vi* finds the word *Bob*. |
| N | Repeats the last / or ? command. |
| Shift+N | Repeats the last / or ? command but reverses the direction of the search. |