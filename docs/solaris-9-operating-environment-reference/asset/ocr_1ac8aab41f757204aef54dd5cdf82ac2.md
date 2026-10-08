# 872

# more, page

ju

(Control-U) Scroll backward half a screen of i lines if specified. If you specify i, the current becomes the default for subsequent d and u commands.

i^U

Exit from more (same as q).

ZZ

Examine (display) a new file. If you specify no file, redisplay the current file.

: file

:t tagstring

Go to the tag named by the tagstringargument, and scroll/rewrite the screen with the tagged line in the current position. See the ctags command.

'letter

Return to the position that was previously marked with the name letter.

''

Return to the position whose last move of more than a screen was made. Default to the beginning of the file.

i?![pattern

Search backward in the file for the i-th line containing pattern. The ! to search backward for the i-th line that does not contain pattern.

i/!pattern

Search forward in the file for the i-th line that does not contain the pattern.

!([command]

Invoke a shell or the specified command.

# Usage

See largefile(5) for the description of the behavior of more and page when encountering files greater than equal to 2 Gbytes (**31 bytes).

# Environment Variables

See environ(5) for the description of the following environment variables that affect the execution of more: LC_COLLATE.

For /usr/xpg4/bin/more only: LC_TYPE, LC_MESSAGES, NLPATH, and TERM.

# /usr/xpg4/bin/more

The following environment variables also affect the execution of /usr/xpg4/bin/more.

+   COLUMNS
Override the system-selected horizon size.
EDITOR
Used by the v command to select an editor.
Override the system-selected vertical screen size. The -n option has precedence over LINES in determining the number of lines in a screen.
MORE
A string specifying options. As in a command line, separate the options with blank characters, and start each option specification with a -. Process any command-line options after those specified in MORE as though the command line were:
 $MORE options operands