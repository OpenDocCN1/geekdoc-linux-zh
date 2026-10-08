count is specified, the cursor advances the specified number of sentences (see ().

(	Move back to the beginning of the preceding paragraph. A paragraph is defined by the value of the paragraphs option. A completely empty line and a section boundary (see [[ above) are also interpreted as the beginning of a paragraph. If a count is specified, the cursor moves backward the specified number of paragraphs.

)	Move forward to the beginning of the next paragraph. If a count is specified, the cursor advances the specified number of paragraphs (see ().

I	Requires a preceding count; the cursor moves to the specified column of the current line (if possible).

+	Move to the first nonwhitespace character in the next line. If a count is specified, the cursor advances the specified number of lines (same as ^M).

,	The comma (,) performs the reverse action of the last f, F, t, or T command issued, by searching in the opposite direction on the current line. If a count is specified, the cursor repeats the search the specified number of times.

-	The hyphen character (-) moves the cursor to the first nonwhitespace character in the previous line. If a count is specified, the cursor moves back the specified number of times.

-	The underscore character (_) moves the cursor to the first nonwhitespace character in the current line. If a count is specified, the cursor advances the specified number of lines, with the current line being counted as the first line; no count or a count of 1 specifies the current line.

.	Repeat the last command that changed the buffer. If a count is specified, the command is repeated the specified number of times.

/	Read a string from the last line on the screen, interpret it as a regular expression, and scan forward for the next occurrence of a matching string. The search begins when the user types a carriage return to terminate the pattern; the search can be terminated by sending SIGINT (or the user-designated interrupt character).

When used with an operator to specify an extent of text, the defined region begins with the current cursor position and ends at the beginning of the matched string. Entire lines can be specified by giving an offset from the matched line (by using a closing / followed by a +n or -n).

0	Move to the first character on the current line (the 0 is not interpreted as a command when preceded by a nonzero digit).

:	The colon character (:) begins an ex command. The: and the entered command are echoed on the bottom