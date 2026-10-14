# Miscellaneous

R or CTRL-L
Redraw (or “repaint”) the screen.

H
Display a help screen.

V
Open the file in the Vi editor, so you can edit it. (Then, when you write and save it with :wq or just exit with :q, you will be back in less.)

Q
Quit viewing the file and exit less.

NOTES: less has many command line options as well as key commands to be used while running, and there are all kinds of tricks you can do with it—almost enough for a whole chapter. If this sort of thing interests you, it’s worth reading through the less man page.

# 9.1.1 Perusing a Text File

To peruse or page through a text file, give the name of the file as an argument to less.

⇒ To page through the text file README, type:
$ less README RET

This command starts less and displays the file README on the screen.

You can move forward through the document a line at a time by typing ↓, and you can move forward through the document a screenful at a time by typing PgDn. To move backward by a line, type ↑, and type PgUp to move backward by a screenful.

You can also search through the text you are currently perusing—this is described in Recipe 14.11 [Searching the Text You’re Perusing], page 354. To stop viewing the file and exit less, press Q.

# 9.1.2 Perusing Text with a Prompt

When you peruse a text file with less, it displays a default prompt at the bottom of the screen with the name of the file in inverse video. As soon as you touch a key, the prompt disappears.

Use the -M option to display a long prompt line, containing the file name, the current and total lines, and the percentage into the file the current line is at. This prompt remains as you move through the text.