set to \(\) after the first time through the loop (after the \(\) has been processed). The last line of the table shows the final values of the variables when the end of the string is reached. You should spend some time studying this table, verifying the values of the indicated variables against the logic of the \(\) function. After this has been accomplished, you should then feel comfortable with the algorithm that is used by the function to count the number of words in a string.

| i | string[i] | wordCount | lookingForWord |
|---|-----------|-----------|----------------|
|   |           | 0         | true           |
| 0 | 'W'       | 1         | false          |
| 1 | 'e'       | 1         | false          |
| 2 | 'l'       | 1         | false          |
| 3 | 'l'       | 1         | false          |
| 4 | ','       | 1         | true           |
| 5 | ' '       | 1         | true           |
| 6 | 'h'       | 2         | false          |
| 7 | 'e'       | 2         | false          |
| 8 | 'x'       | 2         | false          |
| 9 | 'e'       | 2         | false          |
| 10| ' '       | 2         | true           |
| 11| 'g'       | 3         | false          |
| 12| 'o'       | 3         | false          |
| 13| 'e'       | 3         | false          |
| 14| 'g'       | 3         | false          |
| 15| '.'       | 3         | true           |
| 16| '\0'      | 3         | true           |

Table 9.1 Execution of the \(\) Function

# The Null String

Now consider a slightly more practical example of the use of the \(\) function. This time, you make use of your \(\) function to allow the user to type in multiple lines of text. The program then counts the total number of words in the text and displays the result.

To make the program more flexible, you do not limit or specify the number of lines of text that are entered. Therefore, you must have a way for the user to “tell” the program when he is done entering text. One way to do this is to have the user simply press the Enter (or Return) key an extra time after the last line of text has been entered. When the \(\) function is called to read in such a line, the function immediately encounters the newline character and, as a result, stores the null character as the first (and only) character in the buffer. Your program can check for this special case and can know that the last line of text has been entered after a line containing no characters has been