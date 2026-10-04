# 2.3 Evaluating Tcl Script Files

# Example 2.3.1-1

# Script Code

```
puts "This is a simple command"
puts "this line has two"; puts "commands on it"
puts "this line is continued \
on the next line, but prints one line
```

# Script Output

This is a simple command
this line has two
commands on it
this line is continued  on the next line, but prints one line

Note that there are two spaces between the words continued and on. When the Tcl interpreter evaluates a line with a backslash in it, it replaces the backslash newline combination with a space.

You can write Tcl/Tk programs with any editor that will let you save a flat ASCII file. On the Macintosh, the interactive command window behaves like a standard Macintosh editing window, allowing you to scroll back, copy lines, and save text. Under Unix and Windows, the interactive window does not support these options, and you'll need to use a separate editor to create and modify your scripts.

In the Unix world, vi and Emacs are common editors. Notepad, Brief, WordPerfect, and MS-Word are suitable editors in the Windows world, and Mac-Write and Alpha are suitable for use on the Macintosh. Note that you must specify an ASCII text file for the output and use hard newlines if you use one of the word processor style editors. Tcl cannot read a word processor's native format.

Mike Doyle and Hattie Schroeder developed a nice editor as an example in their book Interactive Web Applications with Tcl/Tk (http://www.eolas.com/). This editor allows you to edit a script, test it within the editor, and save it to disk when you are happy with it. This program is on the CD-ROM included with this book. You may find it useful while you're getting familiar with Tcl. It uses a subset of the Emacs/Brief editor commands and the mouse to position a cursor.