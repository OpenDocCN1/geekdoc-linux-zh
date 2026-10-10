Table 10.1 Cursor Movements in vi

| MOVEMENT WITHIN A LINE | CURSOR MOVES |
| :--- | :--- |
| <Left Arrow> or h | One character to the left |
| <Right Arrow> or l | One character to the right |
| 0 (zero) | To the beginning of the line |
| $ | To the end of the line |

| MOVEMENT AMONG WORDS | CURSOR MOVES |
| :--- | :--- |
| w | To the next word |
| b | Back to the previous word |
| e | To the end of the existing word; if the cursor is already at the end of a word, then it will move to the end of the next word |

| MOVEMENT WITHIN THE SCREEN | CURSOR MOVES |
| :--- | :--- |
| <Up Arrow> or k | One line up |
| <Down Arrow> or j | One line down |
| H | To the beginning of the top line on the screen |
| M | To the beginning of the middle line on the screen |
| L | To the beginning of the last line on the screen |

| SCROLLING AMONG SCREENS IN THE SAME FILE | CURSOR MOVES |
| :--- | :--- |
| <Ctrl>-f | Forward to the top of the next screen |
| <Ctrl>-b | Backward to the bottom of the previous screen |

| GENERAL MOVEMENT WITHIN THE FILE | CURSOR MOVES |
| :--- | :--- |
| 1G | To the first line of the file |
| xxG | To line number xx of the file. Substitute the line number you want to travel to. |
| G | To the last line of the file |