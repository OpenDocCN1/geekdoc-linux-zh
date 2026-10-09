# **info**

What it does: Provide system information using a hypertext modality.

Syntax: **info** [*topic*]

Example 1: **info** by itself will open an introductory screen from which you can type “h” to start a tutorial on **info**.

Example 2: **info bash** will provide information about this shell.

Example 3: **info cp** will provide information about the command cp.

# **less**

What it does: Allows you to control the display of a long file.

Syntax: (1) | *less* (2) **less** *filename*

Example 1: **ls** -l | **less** will pipe the output of the command **ls** -l through **less**. You can use a variety of cursor-movement keys to display the output. **less** gives you much more control over the output than does *more*.

Example 2: **cat** *longfile* | **less** will pipe the output of the command **cat** *longfile* | **less** through **less**.

Example 3: **less** *longfile* has the same effect as Example 2. The command line is simpler.

# **ln**

What it does: Creates a link to another file.

Syntax: **ln** *filename*

Example: The command line **ln** */usr/ronsm/accounts/current* will create a link in the working directory to the file **current** in **ronsm**’s directory accounts.