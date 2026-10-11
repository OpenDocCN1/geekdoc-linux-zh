| **Key** | **Description** |
| :--- | :--- |
| y3w, 3yw | Copies three words (starting from the character the cursor is on) into a temporary buffer in memory for later use |
| yy | Copies the current line into a temporary buffer in memory for later use |
| y3y, 3yy | Copies three lines (starting from the current line) into a temporary buffer in memory for later use |
| y$ | Copies the current line from the cursor to the end of the line into a temporary buffer in memory for later use |
| y^, y0 | Copies the current line from the cursor to the beginning of the line into a temporary buffer in memory for later use |
| p | Pastes the contents of the temporary memory buffer underneath the current line |
| P | Pastes the contents of the temporary memory buffer above the current line |
| J | Joins the line underneath the current line to the current line |
| Ctrl+g | Displays current line statistics |
| u | Undoes the last function (undo) |
| . | Repeats the last function (repeat) |
| /pattern | Searches for the first occurence of pattern in the forward direction |
| ?pattern | Searches for the first occurence of pattern in the reverse direction |
| n | Repeats the previous search in the forward direction |
| N | Repeats the previous search in the reverse direction |

| **Function** | **Description** |
| :--- | :--- |
| :q | Quits from the vi editor if no changes were made |
| :q! | Quits from the vi editor and does not save any changes |
| :wq | Saves any changes to the file and quits from the vi editor |
| :w filename | Saves the current document to a file called filename |
| :!date | Executes the date command using a BASH shell |