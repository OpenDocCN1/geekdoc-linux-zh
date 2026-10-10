never) or auto (or true), in which case colors are used only when the output is to a terminal. Defaults to false.

# color.status

A boolean to enable/disable color in the output of (1). May be set to always, false (or never) or auto (or true), in which case colors are used only when the output is to a terminal. Defaults to false.

# color.status.<slot>

Use customized color for status colorization. <slot> is one of header (the header text of the status message), added or updated (files which are added but not committed), changed (files which are changed but not added in the index), untracked (files which are not tracked by Git), branch (the current branch), nobranch (the color the no branch warning is shown in, defaulting to red), or unmerged (files which have unmerged changes).

# color.ui

This variable determines the default value for variables such as color.diff and color.grep that control the use of color per command family. Its scope will expand as more commands learn configuration to set a default for the —color option. Set it to false or never if you prefer Git commands not to use color unless enabled explicitly with some other configuration or the —color option. Set it to always if you want all output not intended for machine consumption to use color, to true or auto (this is the default since Git 1.8.4) if you want such output to use color when written to the terminal.

# column.ui

Specify whether supported commands should output in columns. This variable consists of a list of tokens separated by spaces or commas:

These options control when the feature should be enabled (defaults to never):

+   - always
+   - always show in columns
+   - never
+   - never show in columns
+   - auto
+   - show in columns if the output is to the terminal

These options control layout (defaults to column). Setting any of these implies always if none of always, never, or auto are specified.

+   - column

fill columns before rows