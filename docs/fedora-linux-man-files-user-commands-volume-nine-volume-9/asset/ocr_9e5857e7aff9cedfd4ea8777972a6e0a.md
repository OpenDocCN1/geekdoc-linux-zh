+   -v
+   viminfo file. The optional nuer N is the value for `verbose`. Default is 10.
+   -vi
+   Start **Vim** in Vi mode, just like the executable was called “vi”. This only has effect when the executable is called “ex”.
+   -w {scriptout}
+   All the characters that you type are recorded in the file {scriptout}, until you exit **Vim**. This is useful if you want to create a script file to be used with “vim -s” or “:source!”. If the {scriptout} file exists, characters are appended.
+   -W {scriptout}
+   Like -w, but an existing file is overwritten.
+   -x
+   Use encryption when writing files. Will prompt for a crypt key.
+   -X
+   Don’t connect to the X server. Shortens startup ti in a terminal, but the window title and clipboard will not be used.
+   -y
+   Start **Vim** in easy mode, just like the executable was called “evim” or “eview”. Makes **Vim** behave like a click-and-type editor.
+   -Z
+   Restricted mode. Works like the executable starts with “r”.
+   —
+   Denotes the end of the options. Argurts after this will be handled as a file na. This can be used to edit a filena that starts with a `-’.
+   —echo-wid
+   GTK GUI only: Echo the Window ID on stdout.
+   —help
+   Give a help ssgne and exit, just like “-h”.
+   —literal
+   Take file na argunts literally, do not expand wildcards. This has no effect on Unix where the shell expands wildcards.
+   —noplugin
+   Skip loading plugins. Implied by -u NONE.
+   —remote
+   Connect to a Vim server and make it edit the files given in the rest of the arguments. If no server is found a warning is given and the files are edited in the current Vim.
+   —remote-expr {expr}
+   Connect to a Vim server, evaluate {expr} in it and print the result on stdout.
+   —remote-send {keys}
+   Connect to a Vim server and send {keys} to it.
+   —remote-silent
+   As —remote, but without the warning when no server is found.
+   —remote-wait
+   As —remote, but Vim does not exit until the files have been edited.
+   —remote-wait-silent