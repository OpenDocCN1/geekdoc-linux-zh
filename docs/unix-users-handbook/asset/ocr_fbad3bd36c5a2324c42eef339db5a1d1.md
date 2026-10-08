# ## Character

The fourth basic data type recognized by the C language is the *character type*. Characters can be letters of the alphabet, one of the ten digits 0 through 9, and special symbols such as ! * $ , + @. A single character consists of any one letter, digit, or special symbol enclosed by single quotes. For example:

‘A’   ‘g’   ‘r’   ‘!’   ‘+’   ‘c’

A variable of type character is declared as follows:

```
char letter_grade;
```

Do not confuse single characters with a string of characters.

For example, the single characters ‘B’, ‘e’, ‘a’, ‘c’, ‘h’ are different from the string “Beach.” Each of the letters represented as ‘B’, ‘e’, ‘a’, ‘c’, ‘h’ is viewed by the computer as a separate letter, in spite of the fact that we may automatically read the word Beach. The ‘B’ may be stored in one place in memory, the ‘e’ may be somewhere else, and so on. The computer sees each letter as its own logical unit.

Because humans read the word Beach, C language gave us a way to logically lump the characters together into a “word” or string. A string consists of a series of characters, digits between 0 and 9, and special characters, surrounded by double quotes (“ “). The characters in the “Beach” string are actually stored contiguously inside the computer, or one next to the other. C language makes our job a little easier by supplying a standard set of string functions for use since it would be difficult to deal with each character individually. We will learn more about strings a little later.

# ## Void

The data type of void is a generic data type that has no specific size or range of values associated with it. A void value is nonexistent, values cannot be stored in a variable of the data type void. If you attempt to assign a value to it, the compiler will issue an error message.