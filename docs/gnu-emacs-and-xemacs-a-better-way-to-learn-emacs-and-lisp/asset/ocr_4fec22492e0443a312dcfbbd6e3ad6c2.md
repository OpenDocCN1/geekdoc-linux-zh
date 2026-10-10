inserts the matching closing brace and leaves the cursor between them. CPerl uses more than the standard font-lock faces, which you might already have customized. These new faces are listed in a subgroup of the CPerl Customize group.

Customize is an indispensable part of Emacs, and I’d hate to do without it, but when experimenting with a new package, you might want to fool around with different combinations of settings without bringing up a Customize buffer. The developers of CPerl-mode realized this and built into the mode a way to let you quickly try out several settings via menu choices.

The various indentation styles, such as K&R and GNU, were introduced earlier. Similar styles are used in Perl programming as well. The Indent styles... submenu lets you toggle any of seven different styles. This is especially handy if you haven’t yet settled on a style, because you can quickly change from one to another in order to compare them.

You can use the Toggle submenu to try out various “electric” features, such as electric parentheses and keywords. You can also turn on the auto-newline, similar to cc-mode’s auto-newline, discussed earlier.

All in all, considering the built-in documentation and the abundance of menu commands, CPerl-mode is surely one of the more user-friendly Emacs programming modes.

# # Python Mode

Python is an up-and-coming interpreted scripting language with some similarity to Perl. It is an object-oriented language, like C++ and Java, but it uses an entirely different syntax than those two or Perl. Rather than use curly braces, brackets, or parentheses to separate statements or code blocks from one another, Python uses nothing but indentation levels to group statements under a header. Indentation control is a large part of cc-mode and CPerl-mode, but only for reasons of convention and readability. In Python, the Python interpreter uses white space in order to make sense of the source code. A Python mode for Emacs should make it easy to create and maintain consistent levels of indentation, as well as provide font locking and keyboard/menu commands.

Barry Warsaw’s python-mode.el does all this and more. The standard Python mode for XEmacs, this mode has been under active development for years and is continually being improved as the relatively new Python language evolves. It works fine in GNU Emacs as well. For some reason, it has never been included in the official GNU Emacs distribution, but you can drop a copy of python.el in your