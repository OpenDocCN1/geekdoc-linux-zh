# man – THE ONLINE MANUAL FOR ALL COMMANDS 71

The optional specification of an area limits the search for man texts to a subject area – for example, man 3. This becomes necessary if several homonymous man texts exist in different subject areas. Otherwise, man would only display the first man text found.

> If the -f and -l options the whatis and apropos commands do not work, probably means that a database containing man contents information is missing. You can remedy this by executing `/usr/sbin/makewhatis`. (This program is fairly CPU-intensive.)

In many Unix and Linux books, commands are shown together with their man – for example, find(1). Thus, you straight away how to call man. man knows the subject areas 1 to n. (Sometimes, programming language commands are assigned additional areas with different letters.)

+   - user commands
- system calls
- programming language functions
- file formats, device files
- configuration files
- games
- miscellaneous
- system administration commands
- kernel functions
- new commands

If you want to read all homonymous man texts (of all subjects), you have to man with the option -a. Then man displays the first man text found. As soon as you have read the text and exited man with Q, the man text for the following subject is displayed.

As soon as man text is displayed on screen, the following keyboard shortcuts, amongst many others, are available to navigate through the text (if less has been specified as the default display program in `/usr/lib/man.config`):

# man keyboard shortcuts

| ← | scroll text up or down |
| Home End | jump to the beginning/end of the text |
| Y E | line up or down |
| U D | jump to the beginning/end of the text |
| G Shift+G | search forward |
| / pattern ← | search backward |
| ? ← | repeat search forward/backward |
| N | repeat search backward |
| Shift+N | |
| Q | quit |
| H | display help text with additional keyboard shortcuts |