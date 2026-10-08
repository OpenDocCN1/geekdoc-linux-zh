
# Advanced Bash-Scripting Guide

It consists of nothing more than COMMAND <<< $WORD,
where $WORD is expanded and fed to the stdin of COMMAND.

As a simple example, consider this alternative to the echo-grep construction.

```bash
# Instead of:
if echo "$VAR" | grep -q txt
# if [[ $VAR = *txt* ]]
# etc.
```

```bash
# Try:
if grep -q "txt" <<< "$VAR"
then
  echo "$VAR contains the substring sequence $txt"
fi
# Thank you, Sebastian Kaminski, for the suggestion.
```

Or. in combination with read:

```bash
String="This is a string of words."
read -r -a Words <<< "$String"
# The option to read to successive members of an array
# assigns the resulting values to an array.
```

```bash
echo "First word in String: ${Words[0]}" # This
echo "Second word in String: ${Words[1]}" # is
echo "Third word in String: ${Words[2]}" # a
echo "Fourth word in String: ${Words[3]}" # string
echo "Fifth word in String: ${Words[4]}" # string
echo "Sixth word in String: ${Words[5]}" # words.
echo "Seventh word in String: ${Words[6]}" # (null)
# Past end of $String.
```

Thank you, Francisco Lobo, for the suggestion.
it is, of course, possible to feed the output of a here string into the stdin of loop.

```bash
# As Seamus points out =
ArrayVar=$(element0 element1 element2 {A..D})

while read element; do
  echo "$element" 1>&2
done <<< $(echo ${ArrayVar[*]})

# element0 element1 A B C D
```

# Example 19-13. Prepending a line to a file

```bash
#!/bin/bash
# prepend. Add text at beginning of file.
# Example contributed by Kenny Stauffer,
# + slightly modified by document author.
```

```bash
E_NOSUCHFILE=85
```

Chapter 19. Here Documents

# Advanced Bash-Scripting Guide

```bash
read -p "File: " file # -p arg to 'read' displays prompt.
if [ -e "$file" ]
then # Bail out if no such file.
echo "File $file not found."
exit $E_NOSUCHFILE
fi
```

```bash
read -p "Title: " title
cat $file <<<$title > $file.new
```

```bash
echo "Modified file is $file.new"
```

```bash
exit # Ends script execution.
```

from 'man bash':
Here Strings
A variant of documents, the format is:

<<Word

The word is expanded and supplied to the command on its standard input.

Of course, the following also works:
sed -e '!!i'
Title: '$file'

# Example 19-14. Parsing a mailbox

```bash
#!/bin/bash
# Script by Francisco Lobo,
#+ and slightly Modify and commented by ABS Guide author.
# Used in ABS Guide with permission. (Thank you!)
```

```bash
# This script will not run under Bash versions -lt 3.0.
```

```bash
E_MISSING_ARG=87
if [ -z "$1" ]
then
echo "Usage: $0 mailbox-file"
exit $E_MISSING_ARG
fi
```

```bash
mbox_grep() # Parse mailbox file.
{
  declare -i body=0 match=0
  declare -a date sender
  declare mail header value
```

```bash
while IFS= read -r mail
# Reset IFS.
# Otherwise "read" will strip leading & trailing space from its input.

  if [[ $mail =~ ^From ]]; # Match "From" field in message.
then
    (( body = 0 )) # "Zero out" variables.
    (( match = 0 ))
```

Chapter 19. Here Documents

# Advanced Bash-Scripting Guide

```bash
elif (( body ))
then
    (( match ))
    # echo "mail"
    # Uncomment above line if you want entire body
    +# of message to display.
```

```bash
elif [[ $mail ]]; then
IFS=- read -r header value <<< "$mail"
#                               "here string"

case "$header" in
    [Ff][Rr][Oo] [Mm]) [[ $value = "$2" ]] && (( match++));
    # Match "From"
    [Dd][Aa][Tt] [Ee]) read -r -a date <<< "$value";
    # Match "Date" line.
    [Rr][Ee][Cc] [Ei][Ii] [Vv][Ee] [Dd]) read -r -a sender <<< "$value"; # Match IP Address (may be spoofed).
```

```bash
else
    (( body ))
    (( match )) &&
    echo "MESSAGE ${date+of: ${date[*]}}"
    # Entire $date array
    echo "IP address of sender: ${sender[1]}"
    # Second field of "Received" line
```

```bash
fi

done < "$1" # Redirect stdout of file into loop.
```

```bash
mbox_grep "$1" # Send mailbox file to function.
```

```bash
exit $?
```

+   # Exercises:
#-
# 1) Break the single function,
#-
# 2) Use the mailbox parser to count messages by sender.
# 3) Use here strings to pass variables to functions.

# 1) Break the single function,
#-
# 2) Use the mailbox parser to count messages by sender.
# 3) Use here strings to pass variables to functions.

# 1) Break the single function,
#-
# 2) Use the mailbox parser to count messages by sender.
# 3) Use here strings to pass variables to functions.

# 1) Break the single function,
#-
# 2) Use the mailbox parser to count messages by sender.
# 3) Use here strings to pass variables to functions.

# 1) Break the single function,
#-
# 2) Use the mailbox parser to count messages by sender.
# 3) Use here strings to pass variables to functions.
