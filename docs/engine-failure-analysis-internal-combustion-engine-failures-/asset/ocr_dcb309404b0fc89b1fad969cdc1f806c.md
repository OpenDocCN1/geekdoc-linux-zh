# AT A GLANCE (CONT.)

How Do I | Example
Scroll down? | **emacs:** PgDn **joe:** PgDn **pico:** Ctrl + n **vi:** PgDn or j or down arrow
Scroll up? | **emacs:** PgUp **joe:** PgUp **pico:** Ctrl + p **vi:** PgUp or k or up arrow
Search for text? | **emacs:** Ctrl + s **joe:** Ctrl + k, f **pico:** Ctrl + #w **vi:** /pattern
See the program’s keyboard shortcuts on-screen? | **emacs:** F1 **joe:** Ctrl + k, h **pico:** Ctrl + g **vi:** F1
Split the screen into two windows? | **emacs:** Ctrl + x, 3 **joe:** Ctrl + k, o **vi:** :sp
Undo an editing change? | **emacs:** Ctrl + _ **joe:** Ctrl + _ **vi:** u

# Specifying the Default Editor

To determine the default editor currently in use, type `echo $EDITOR` and press Enter; you’ll see the path name to the default editor, if any. Should you wish to change the default editor, do the following:

+   1.  In your home directory, use a text editor to open the file named `.bash_profile`.