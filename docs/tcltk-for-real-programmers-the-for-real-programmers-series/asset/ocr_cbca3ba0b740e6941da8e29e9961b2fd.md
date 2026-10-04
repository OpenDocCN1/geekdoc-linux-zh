# 4.3 Looking for a Needle in a Haystack

| Definition | Example | Description |
| --- | --- | --- |
| An atom | T | If the atom is matched, the regular expression is true. |
| A piece | [CcLcl1]* | If the piece is matched, the regular expression is true. |
| Multiple pieces separated by "|" | ([Tt]c1) | ([Tt]k) | If any piece is matched, the regular expression is true. |

The range atom [[a-z]] needs a little more explanation, since there are actually several rules to define a range of characters.

A range consists of square brackets enclosing:

| Definition | Example | Description |
| --- | --- | --- |
| A set of characters | [tcl] | Any of the letters within the brackets may match the target. |
| Two characters separated by a dash | [a-z] | The letters define a range of characters that may match the target. |
| A character preceded by a caret, if the caret is the first letter in the range | [^,] | Any character except the character after the caret may match the target. |
| Two characters separated by a dash and preceded by a caret, if the caret is in the range | [^a-z] | Any character except characters between the two characters after the caret may match the target. |

A piece or atom can be enclosed within parentheses and then will be considered as a single atom. For instance,
[[a-z][0-9]]+

would look for repeating patterns of a single letter followed by a single digit and would match one or more of these letter-number patterns.

The regular expression commands will return the largest block of text that matches the regular expression. Thus a regular expression such as:

A.+B