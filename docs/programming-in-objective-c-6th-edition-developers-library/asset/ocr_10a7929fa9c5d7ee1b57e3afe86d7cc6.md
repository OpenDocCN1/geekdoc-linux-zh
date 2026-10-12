It might seem that the preceding program does not help to reduce your work efforts much because you still have to manually enter all of the text at the terminal. But as you will see in **Chapter 15**, “*Input and Output Operations in C*,” this same program can also be used to count the number of words contained in a file stored on a disk, for example. So, an author using a computer system for the preparation of a manuscript might find this program extremely valuable as it can be used to quickly determine the number of words contained in the manuscript (assuming the file is stored as a normal text file and not in some word processor format like Microsoft Word).

# # Escape Characters

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

The first seven characters listed in **Table 9.2** perform the indicated function on most output devices when they are displayed. The *audible alert* character, \a, sounds a “bell.” So, the \p *call p* Click here to view code image sounds an alert and displays the indicated message. Including the backspace character '\b' inside a character string causes the terminal to backspace