![](bbox=[0.03, 0.09, 0.12, 0.2])

# pg - File viewing filter.

pg(1) pg(1) NAME pg - file persual filter for soft-copy terminals

SYNOPSIS pg [-number] [-pstring] [-cefns] [+linenumber] [/pattern] [file ...]

Remarks pg and more are both used in similar situations (see more(1)). Text highlighting features supported by more are not available from pg. However, pg has some useful features not provided by more.

DESCRIPTION pg is a text file filter that allows the examination of files one screenful at a time on a soft-copy terminal. If - is used as a file argument, or pg detects NULL arguments in the command line, the standard input is used. Each screenful is followed by a prompt. To display a new page, press Return. Other possibilities are enumerated below.

This command is different from other paginators such as more in that it can back up for reviewing something that has already passed. The method for doing this is explained below.

In order to determine terminal attributes, pg scans the terminfo database for the terminal type specified by the environment variable TERM (see terminfo(4)). If TERM is not defined, terminal type dumb is assumed.

Options pg recognizes the following command line options:

+   - -number
number is an integer specifying the size (in lines) of the window that pg is to use instead of the default (on a terminal containing 24 lines, the default window size is 23).
- -p string
Causes pg to use string as the prompt. If the prompt string contains a $, the first occurrence of $ in the prompt is replaced by the current page number when the prompt is issued. The default prompt string is a colon (:
- -c
Home the cursor and clear the screen before displaying each page. This option is ignored if clear_screen is not defined in the terminfo database for this terminal type.
- -e
Causes pg to not pause at the end of each file.
- -f
Normally, pg splits lines longer than the screen