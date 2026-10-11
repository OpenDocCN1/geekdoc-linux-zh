```
$ cat read3
read -p "Enter something: " word1 word2 word3
echo "Word 1 is: $word1"
echo "Word 2 is: $word2"
echo "Word 3 is: $word3"
$ read3
Enter something: **this is something**
Word 1 is: this
Word 2 is: is
Word 3 is: something
```

When you enter more words than read has variables, read assigns one word to each variable, with all leftover words going to the last variable. Both **read1** and **read2** assigned the first word and all leftover words to the one variable they each had to work with. In the following example, **read** accepts five words into three variables, assigning the first word to the first variable, the second word to the second variable, and the third through fifth words to the third variable:

```
$ read3
Enter something: **this is something else, really.**
Word 1 is: this
Word 2 is: is
Word 3 is: something else, really.
```

Table 27-4 lists some of the options supported by the read builtin.

**Table 27-4** read options
| Option | Function |
| :--- | :--- |
| **--a** *anarray* (array) | Assigns each word of input to an element of array *anarray* . |
| **--d** *delim* (delimiter) | Uses *delim* to terminate the input instead of NEWLINE. |
| **-e** (Readline) | If input is coming from a keyboard, use the Readline Library (page 326) to get input. |
| **-n** *num* (number of characters) | Reads *num* characters and returns. As soon as the user types *num* characters, read returns; there is no need to press RETURN. |
| **-p** *prompt* (prompt) | Displays *prompt* on standard error without a terminating NEWLINE before reading input. Displays *prompt* only when input comes from the keyboard. |
| **-s** (silent) | Does not echo characters. |
| **-u n** (file descriptor) | Uses the integer *n* as the file descriptor that read takes its input from. |

read -u4 arg1 arg2
is equivalent to
read arg1 arg2 <&4
See “File Descriptors” (page 921) for a discussion of redirection and file descriptors.