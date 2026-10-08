# 328

Address Description
% 1,$.

The ex initialization options are listed below.

Option Description
$HOME/.exrc Editor initialization file.
./.exrc Editor initialization file.
EXINIT Place set commands in the EXINIT environment variable.
set Show changed options.
set al Show all options.
set nox Disable option x.
set x Enable option x.
set x=val Give value val to option x.
set x? Show value of option x.

The most useful ex options and their abbreviations are listed below.

Option Abbrev. Description
autointend ai Supply indent.
autowrite aw Write before changing files.
directory Path name of directory for temporary work files.
ex ex Enable vi/ex to read the .exrc in the current directory. This option is set in the EXINIT shell variable or in the ex file in the $HOME directory.
ignorecase ic Ignore case of letters in scanning. Note that there is no easy way to do a single scan ignoring case.
list Print *1 for Tab, $ at end.
magic Treat .* as special in patterns.
modelines Execute first five lines and last five lines as vi/ex commands if they are of the form ex:command: or vi:command.
number nu Number lines.
agraphs para Macro names that start paragraphs.
redraw Simulate smart terminal.
report Inform you if the number of lines modified by the last command is greater than the value of the report variable.
scroll Command-mode lines.