# Introducing sed and gawk

# IN THIS CHAPTER

+   * Manipulating text
+   * Looking at the `sed` editor basic commands

y far, one of the most common functions for which people use shell scripts is to work with text files. Between examining log files, reading configuration files, and handling data elements, shell scripts can help automate the mundane tasks of manipulating any type of data contained in text files. However, trying to manipulate the contents of text files using just shell script commands is somewhat awkward. If you perform any type of data manipulation in your shell scripts, you want to become familiar with the `sed` and `gawk` tools available in Linux. These tools can greatly simplify any data-handling tasks you need to perform.

# Manipulating Text

Chapter 10, “Working with Editors,” demonstrated how to edit text files using different editor programs available in the Linux environment. These editors enable easy manipulation of text contained in a text file by using simple commands or clicks of the mouse.

There are times, however, when you’ll find yourself wanting to manipulate text in a text file on the fly, without having to pull out a full-fledged interactive text editor. In these situations, it’s useful to have a simple command-line editor that can easily format, insert, modify, and delete text elements automatically.

The Linux system provides two common tools for doing just that. This section covers the two most popular command-line editors used in the Linux world, `sed` and `gawk`.

# Getting to know the `sed` editor

The `sed` editor is called a *stream editor*, as opposed to a normal interactive text editor. In an interactive text editor, such as `vim`, keyboard commands are used interactively to insert, delete, or replace text in the data. A stream editor edits a stream of data based on a set of rules supplied ahead of time.