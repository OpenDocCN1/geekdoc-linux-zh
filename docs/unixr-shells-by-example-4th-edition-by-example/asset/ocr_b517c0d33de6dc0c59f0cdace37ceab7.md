# Table 15.3 Common C/Shell Error Messages (continued)

| Error Message | What Caused It | What It Means | How to Fix It |
| Too many 's | if $x = $y && $x != 3 ) then
if $x = $y && $x != 3 ) then | The expression has unbalanced parentheses. Either add the right-hand side or remove the && after the ( | if ( $x = $y && $x != 3 ) then
or if $x = $y && $x != 3 ) then |
| top: label not found. | goto top | The goto command is looking for a label called top that should be on a line by itself somewhere in the program. Either that label is itself somewhere but spelled differently. | top:
goto top |
| undefined variable | echo $name | The variable name has never been set. | set name = "John";
set name = $name |
| unmatched " | echo "She said, "Hello" | The double quote must be matched on the same line. | echo "She said, "Hello" |
| unmatched ' | echo 'I don't care' | The single quote must be matched on the same line. | echo 'I don't care' |
| while: Expression syntax. | while ( $n <= 5 ) | The wrong operator was used. It should be <= | while ( $n <= 5 ) |

# Table 15.4 Common Bourne Shell Error Messages.

# Common Bourne Shell Error Messages

Table 15.4 lists commonly found Bourne shell error messages.

# Table 15.4 Common Bourne Shell Error Messages

| Error Message | What Caused It | What It Means | How to Fix It |
| (file): syntax error near 'case' | case "blue" | The case command is missing the in keyword. | case $color in |
| (file): syntax error near 'case' | case $color | The variable doesn't exist or is empty. | name="some value" |
| (blank line): no error message. | blank line | There must be a space after the { | if [ $USER = "elfie" ] ; then |
| [elfie]: not found | if [ $USER = "elfie" ] ; then | There cannot be any space on either side of the equal sign. | answer="Yes" |
| answer: not found | answer = "Yes" | | |