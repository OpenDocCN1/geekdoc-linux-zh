# 15.4 Probable Causes for Syntax Errors

# Table 15.6 Common Bash Shell Error Messages.

# Table 15.6 lists commonly found Bash shell error messages.

| Error Message | What Caused If | What If Means | How to Fix It |
|---|---|---|---|
| bash: syntax error: unexpected EOF while looking for matching `"` | echo I don't care | The single quote is unmatched in the script. | echo "I don't care" |
| bash: syntax error: unexpected EOF while looking for matching `'` | print She said "Hello" | The double quote is unmatched in the script. | print She said 'Hello' |
| [Blank line] No error message, no output | echo $name or echo ${Fruit[5]} | The variable doesn't exist or is empty. | name="some value" or use -d to catch any variables that have not been set. The message will be printed later if the SET is sent to stderr. |
| bash: name: command not found | name="Tom" | There cannot be any space on either side of the equal sign | name=Tom |
| bash: 8.5: syntax error in expression (error token is ".5") | declare -i num=8.5 | Only integer values can be assigned to variable num | num=6 |
| bash: [Ellie]: command not found | if [[ $USER = "Ellie" ]]; then or if [[ $USER = "Ellie" ]]; then | These must be a space after the [[ or [[ | if [[ $USER = "Ellie" ]]; then |
| bash: syntax error near unexpected token `fi' | if [[ $USER = "Ellie" ]]; then if [[ $USER = "Ellie" ]]; then if [[ $USER = "Ellie" ]]; then if [[ $USER = "Ellie" ]] | The then should be on the next line or preceded by a semicolon | if [[ $USER = "Ellie" ]]; then |
| bash: syntax error in conditional expression | if [[ $name = "John Doe" ]]; then | Word splitting is not performed on the right-hand side of the =", but the string on the left-hand side must be quoted. | if [[ "$name" = "John Doe" ]]; then |
| [: fret: binary operator expected | if [ grep Fred /etc/passwd ]; then | The grep command should not be surrounded by square brackets on any other symbols. The brackets are used only when testing expressions. The [ is a test operator. | if grep Fred /etc/passwd; then |