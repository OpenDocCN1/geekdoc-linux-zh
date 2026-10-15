
# Table 15.5 Common Korn Shell Error Messages (continued)

## 15.4 Probable Causes for Syntax Errors

| Error Message | What Caused It | What It Means | How to Fix It |
|---|---|---|---|
| [blank line] | echo $name or echo ${fruit[5]} | The variable doesn't exist or is empty. | name="Some value" |
| file2: line2: syntax error at line 6: `done' unexpected | while (( $n < 5 )) do statements done | The while is missing the do keyword | while (( $n < 5 )) do statements done |
| file: syntax error at line 3: unmatched | print I don't care | The single quote is unmatched in the script. It should be enclosed in double quotes. | echo "I don't care" or echo 'I don't care' |
| file: syntax error at line 3: unmatched | print She said Hello | The double quote is unmatched in the script. | print She said "Hello" |
| ksh: [: Doe: unknown operator | name="John Doe"; then if [ $name = Joe ]; then or if [[ $name == Joe ]]; then | The variable `name' should be double quoted in the test expression. There can be only one string on the left-hand side of the = test operator. The other alternative will not be used when using this operator. Words will be split when using the [ or [[. | if [ "$name" = Joe ]; then or if [[ $name == Joe ]]; then |
| ksh: [ellie: not found | if [ $USER = "ellie" ]; then if [[ $USER = "ellie" ]]; then | There must be a space after the [ or [[ operator. | if [ $USER = "ellie" ]; then if [[ $USER = "ellie" ]]; then |
| ksh: apples: bad number | set -a; apples pears peaches fruit | The shift built-in command shift can only shift positional parameters used only in shift command. | set apples pears peaches fruit |
| -ksh: file.exe-foo: not found | file.exe-foo | The variable cannot have a period in its name. | file.exe-foo |
| ksh: file: file already exists. | sort file > temp | The nodobber variable has been set and the temp file exists. | sort file > temp (use a different file for output) or sort file > temp (override nodobber) or nodobber will not let you overwrite an existing file. |

| Error Message | What Caused It | What It Means | How to Fix |
|---|---|---|---|
| ksh: fred: unknown test operator if [ grey fred /etc/passwd ] ; then | if [ grey fred /etc/passwd ] ; then | The grep command should not be surrounded by square brackets or any other symbols. The brackets are used only when testing expressions. The ! is a test operator. | if grep fred /etc/passwd ; then |
| ksh: name: not found name = "Tom" | name = "Tom" | There is no space to be built in command or used to shift positional parameters. The built-in command is either equal sign. | set name "Tom" |
| ksh: shift: bad number shift 2 | shift 2 | The shift command will shift apples and pears will be shifted from the list. There should be at least two positional parameters. If there will not fall. | apples 2 |
| ksh: syntax error: "echo hi" not expected | function fun { echo "hi"; } | There should be space surrounding the curly braces in the definition of the function (fun). The semicolon will terminate the function statement. | function fun { echo "hi"; } |
| ksh: syntax error: "Doe" unexpected if [[ $name = "John Doe" ]] | if [[ $name = John Doe ]] | Word splitting is not performed on the left-hand side of the = but the string on the right-hand side must be quoted. | if [[ $name = "John Doe" ]] |
| ksh: syntax error: "fi" unexpected if [ USER = "ellie" ] then or | if [ USER = "ellie" ] then or | The then should be on the next line or preceded by a semicolon. | if [ USER = "ellie" ] then |
| ksh: syntax error: "then" unexpected if (( $a == $b )) | if (( $a == $b )) | The parentheses enclosing the second expression are not matched. | if (( $a == $b )) |
| ksh: trap: 500: bad trap trap 'm trap' 500 | trap 'm trap' 500 | The number 500 is an illegal signal. Normally signals 2 or 3 will be trapped in a shell script. 2 is for Ctrl-C and 3 is for Ctrl-Y. Both cause the program named after the trap command to be terminated. | trap 'm trap' 2 |

# Table 15.5 Common Korn Shell Error Messages (continued)

a. This error occurs with public domain Korn shell, but Korn shell 88 (Solaris) produces no output.
