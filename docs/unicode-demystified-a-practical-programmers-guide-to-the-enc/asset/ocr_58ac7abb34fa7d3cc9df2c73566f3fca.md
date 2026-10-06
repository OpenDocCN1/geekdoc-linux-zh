# Search and Replace Examples

:s/bigger/biggest/
places the string bigger on the current line with biggest
Example:
bigger → biggest

:1..s/Ch 1/Ch 2/g
places every occurrence of the string Ch 1, before or on the current line, with the string Ch 2
Examples:
Ch 1 -> Ch 2
Ch 12 -> Ch 22

:1,$s/ten/10/g
places every occurrence of the string ten by the string 10
Examples:
ten -> 10
often -> 10ant

:g/chapter/s/ten/10/
places the first occurrence of the string ten with the string 10
on all lines containing the word chapter
Examples:
chapter -> chapter 10
chapters will often -> chapters will of

:s\(first\)\(last\)\21/
uses the pattern-holding buffers to swap first and last on the current line
Example:
firstlast -> lastfirst

:%s\<ten>/10/g
places every occurrence of the word ten by the string 10
Example:
ten -> 10

..+10s/every/each/g
places every occurrence of the string every by the string each on the current line through the tenth following line
Examples:
every -> each
everything -> eachthing

:s\<short\>/"&/
places the word short on the current line with "short" (en-closed within quotation marks)
Example:
the shortest of the short -> the shortest of the "short"