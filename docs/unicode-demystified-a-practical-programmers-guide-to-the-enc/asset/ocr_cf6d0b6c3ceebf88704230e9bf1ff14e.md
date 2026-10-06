# Parameters

parameter by giving the command :set [no]param. For example, give the command
set number or :set nonumber to turn on/off line numbering (Table 10-8). To change
t value of a parameter that takes a value (and uses an equal sign), give a com-\mand such as :set shiftwidth=15. Most parameters have abbreviations that you can
use in their place (nu for number and nonu for no number, sw for shiftwidth; the
abbreviations are listed in the left column of Table 10-8.

table 10-8

Line numbers
number, nu

The vim editor does not normally display the line associ-
ated with each line. To display line numbers, set the parameter
To cause line numbers not to be displayed, the param-
ter nonumber.

Line numbers, whether displayed or not, are not part of the file,
are not stored with the file, and are not displayed when the file is
printed. They appear on the screen only when you are using vim.

Line wrap margin
wrapmargin, wm

The wrap margin causes vim to break the text that you are in-
serting at approximately the specified number of characters from
t right margin. The vim editor breaks the text by inserting a NEW-\LINE character at the closest blank-delimited word boundary. Setting the line margin is handy if you want all your text lines to
be the same length. It relieves you of having to remember to
press RETURN to each line of input.

Set the wrapmargin=nn, where nn is the number of
characters from the right side of the screen where you want vim to
break the text. This number is not the column width of the text but
d distance from the end of the text to the right edge of the screen.
Setting wrap margin to 0 (zero) turns this feature off. By default,
vim sets the wrap margin to 0.

Shell
shell, sh

While using vim, you can cause it to spawn a new shell.
You either create an interactive shell (if you want to run several
commands) or run a single command. The shell parameter deter-
m what vim invokes. By default vim sets the shell parametr-
to your login shell. To change it, set the parameter
shell--pathname, where pathname is the full path of the shell
to want to use.

Shell mode
showmode, smd

The vim editor not normally give you a visual cue to let
know when it is Input mode. In some versions of vim, however,
You can set the parameter showmode to display the mode in the
lower-right corner of the screen when vim is in Input or Command
mode. Three types of input mode are Open, Insert, and Append. Set
showmode to cause vim not to display the message.