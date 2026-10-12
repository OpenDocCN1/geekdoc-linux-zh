
# Program 9.8 Output

Click here to view code image

Wendy glanced up at the ceiling where the mound of lasagna loomed like a mottled mountain range. Within seconds, she was crowned with ricotta ringlets and a tomato sauce tiara. Bits of beef formed meaty moles on her forehead. After the second thud, her culinary coronation was complete.

Return

The line labeled *Return* indicates the pressing of the Enter or Return key.

The `e` variable is used as a flag to indicate when the end of the input text has been reached. The `w` loop is executed as long as this flag is `f`. Inside this loop, the program calls the `r` function to read a line of text. The `i` statement then tests the input line that is stored inside the `t` array to see if just the Enter (or Return) key was pressed. If so, then the buffer contains the null string, in which case the `e` flag is set to `t` to signal that all of the text has been entered.

If the buffer does contain some text, the `c` function is called to count the number of words in the `t` array. The value that is returned by this function is added into the value of `t`, which contains the cumulative number of words from all lines of text entered thus far. After the `w` loop is exited, the program displays the value of `t`, along with some informative text.

It might seem that the preceding program does not help to reduce your work efforts much because you still have to manually enter all of the text at the terminal. But as you will see in **Chapter 15**, “*Input and Output Operations in C*,” this same program can also be used to count the number of words contained in a file stored on a disk, for example. So, an author using a computer system for the preparation of a manuscript might find this program extremely valuable as it can be used to quickly determine the number of words contained in the manuscript (assuming the file is stored as a normal text file and not in some word processor format like Microsoft Word).

## Escape Characters

As alluded to previously, the backslash character has a special significance that extends beyond its use in forming the newline and null characters. Just as the backslash and the letter n, when used in combination, cause subsequent printing to begin on a new line, so can other characters be combined with the backslash character to perform special functions. These various backslash characters, often referred to as *escape characters*, are summarized in **Table 9.2**.

| Escape Character | Name |
| --- | --- |
| \a | Audible alert |
| \b | Backspace |
| \f | Form feed |
| \n | Newline |
| \r | Carriage return |
| \t | Horizontal tab |
| \v | Vertical tab |
| \\ | Backslash |
| \" | Double quotation mark |
| \' | Single quotation mark |
| \? | Question mark |
| \nnn | Octal character value $nnn$ |
| \unnnn | Universal character name |
| \Unnnnnnnn | Universal character name |
| \xnn | Hexadecimal character value $nn$ |

The first seven characters listed in **Table 9.2** perform the indicated function on most output devices when they are displayed. The *audible alert* character, \a, sounds a “bell.” So, the \p *call p* Click here to view code image sounds an alert and displays the indicated message. Including the backspace character '\b' inside a character string causes the terminal to backspace one character at the point at which the character appears in the string, provided that it is supported. Similarly, the function call

Click here to view code image

p displays the value of a, space over to the next tab setting (typically set to every eight columns by default), displays the value of b, space over to the next tab setting, and then displays the value of c. The horizontal tab character is particularly useful for lining up data in columns.

To include the backslash character itself inside a character string, two backslash characters are necessary, so the p

Click here to view code image

p displays the following:

Click here to view code image

Note that because the \ is encountered first in the string, a tab is not displayed in this case. To include a double quotation character inside a character string, it must be preceded by a backslash. So, the p

Click here to view code image

p results in the display of the message "

To assign a single quotation character to a character variable, the backslash character must be placed before the quotation mark. If c is declared to be a variable of type c, the statement

Click here to view code image

assigns a single quotation character to c. The backslash character, followed immediately by a ?, is used to represent a ? character. This is sometimes necessary when dealing with trigraphs in non-ASCII character sets. For more details, consult Appendix A, “C Language Summary.”

The final four entries in Table 9.2 enable any character to be included in a character string. In the escape character ' nn' , nn is a one- to three-digit octal number. In the escape character ' nn' , nn is a hexadecimal number. These numbers represent the internal code of the character. This enables characters that might not be directly available from the keyboard to be coded into a character string. For example, to include an ASCII escape character, which has the value octal 33, you could include the sequence \or \ inside your string.

The null character is a special case of the escape character sequence described in the preceding paragraph. It represents the character that has a value of 0. In fact, because the value of the null character is 0, this knowledge is frequently used by programmers in tests and loops dealing with variable-length character strings. For example, the loop to count the length of a character string in the function s from Program 9.2 can also be equivalently coded as follows:

The value of s is nonzero until the null character is reached, at which point the w loop is exited.

It should once again be pointed out that these escape characters are only considered a single character inside a string. So, the character string " actually consists of nine characters (not counting the terminating null): the character ' , the double quotation character ' , the five characters in the word H , the double quotation character once again, and the newline character. Try passing the preceding character string to the s function to verify that nine is indeed the number of characters in the string (again, excluding the terminating null).

A universal character name is formed by the characters \u followed by four hexadecimal numbers or the characters \U followed by eight hexadecimal numbers. It is used for specifying characters from extended character sets; that is, character sets that require more than the standard eight bits for internal representation. The universal character name escape sequence can be used to form identifier names from extended character sets, as well as to specify 16-bit and 32-bit characters inside wide character string and character string constants. For more information, refer to Appendix A.

## More on Constant Strings

If you place a backslash character at the very end of the line and follow it immediately by a carriage return, it tells the C compiler to ignore the end of the line. This line continuation technique is used primarily for continuing long constant character strings onto the next line and, as you see in Chapter 12, "The Preprocessor," for continuing a macro definition onto the next line.

Without the line continuation character, your C compiler generates an error message if you attempt to initialize a character string across multiple lines; for example:

Click here to view code image

By placing a backslash character at the end of each line to be continued, a character string constant can be written over multiple lines:

Click here to view code image

It is necessary to begin the continuation of the character string constant at the beginning of the next line because, otherwise, the leading blank spaces on the line get stored in the character string. The preceding statement, therefore, has the net result of defining the character array 1 and of initializing its elements to the character string

Click here to view code image

Another way to break up long character strings is to divide them into two or more adjacent strings. Adjacent strings are constant strings separated by zero or more spaces, tabs, or newlines. The compiler automatically concatenates adjacent strings together. Therefore, writing the strings
