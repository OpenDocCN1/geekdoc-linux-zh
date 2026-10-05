NOTE
If vim-enhanced is installed, regular users will have a shell alias so that if they run
t vi command, they will automatically get the vim command instead. This does
not apply to root and other users with UIDs below 200 (which are used by system
services).

If you are editing files as the root and expect vi to run in enhanced mode,
can be a surprise. Likewise, vim-enhanced is installed and a regular user wants
t simple vi for some reason, they might need to use \vi to override the alias	empor.

Advanced users can use \vi --version and vim --version to compare the
feature of the two commands.

# Vim Operating Modes

An unusual characteristic of Vim is that it has several modes of operation, command
mode, extended command mode, edit mode, and visual mode. Depending on the mode, you may
be issuing commands, editing text, or working with blocks of text. As a new Vim user, you should
always be aware of your current mode keystrokes have different effects in different modes.

![](bbox=[0.152, 0.442, 0.846, 0.663])

Figure 5.10: Moving between Vim modes

When you first open Vim, it starts in command mode, which is used for navigation, cut and paste,
or other text manipulation. Enter each of the other modes with single character keystrokes to
pecific editing functionality:

+   - An i keystroke enters insert mode, where all text becomes file content. Pressing Esc
returns to command mode.
- A V keystroke enters visual mode, where multiple characters may be selected for text
ulation. Use Shift+V for multiline and Ctrl+V for block selection. The same keystroke
used to enter visual mode (v, Shift+V or Ctrl+V) is used to exit.
- The colon begins extended command mode for tasks such as writing the file (to save it),
and quitting the Vim editor.