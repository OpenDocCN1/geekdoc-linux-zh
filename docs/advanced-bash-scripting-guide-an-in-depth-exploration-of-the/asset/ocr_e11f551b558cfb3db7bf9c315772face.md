# Advanced Bash-Scripting Guide

```
read -p "File: " file # -p arg to 'read' displays prompt.
if [ -e "$file" ]
then # Bail out if no such file.
echo "File $file not found."
exit $E_NOSUCHFILE
fi
```

```
read -p "Title: " title
cat $file <<<$title > $file.new
```

```
echo "Modified file is $file.new"
```

```
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

```
#!/bin/bash
# Script by Francisco Lobo,
#+ and slightly Modify and commented by ABS Guide author.
# Used in ABS Guide with permission. (Thank you!)
```

```
# This script will not run under Bash versions -lt 3.0.
```

```
E_MISSING_ARG=87
if [ -z "$1" ]
then
echo "Usage: $0 mailbox-file"
exit $E_MISSING_ARG
fi
```

```
mbox_grep() # Parse mailbox file.
{
  declare -i body=0 match=0
  declare -a date sender
  declare mail header value
^^^^^^
```

```
while IFS= read -r mail
# Reset IFS.
# Otherwise "read" will strip leading & trailing space from its input.

  if [[ $mail =~ ^From ]]; # Match "From" field in message.
then
    (( body = 0 )) # "Zero out" variables.
    (( match = 0 ))
```

Chapter 19. Here Documents