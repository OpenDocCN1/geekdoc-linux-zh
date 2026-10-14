⇒ To output only the second field from the file bank-statement, where fields are delimited by a space character, and suppress output of lines not containing this field, type:
$ cut -d " " -f2 bank-statement RET

Fields are output with the same delimiter used in the input. To specify a different delimiter for the output, give it as an argument to the long-style option --output-delimiter.

⇒ To take the third through fifth fields from the file ‘bank-statement,’ where fields are delimited by a space character, and output them delimited by tab characters, type:
$ cut -d " " -f3-5 --output-delimiter CTRL-V TAB
bank-statement RET

To specify bytes or characters in place of fields, use the -b and -c options, respectively.

⇒ To output the first, third, fifth, and seventh characters from each line in the file bank-statement, type:
$ cut -c1,3,5,7 bank-statement RET

# METHOD #2

Use colrm to remove columns in text by their character positions. Given a number as an argument, colrm will remove all text on each line, beginning at that character position.

⇒ To output only the first two characters on each line of the file percentages, type:
$ colrm 3 < percentages RET

If you give an ending column as a second argument, colrm removes all columns from the first to the second arguments, inclusive. The columns to the right of the ending column are brought over to join the column preceding the first argument.

⇒ To output the contents of the file amounts, removing the tenth through sixtieth characters on each line of text, and writing to a file called markdown, type:
$ colrm 10 60 < amounts > markdown RET