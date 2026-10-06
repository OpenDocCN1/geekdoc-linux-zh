# Help Commands (Continued)

+   - CONTROL-H k key-sequence: Prints the name and documentation of the command bound to key-sequence. (See the notes on the preceding command.)

+   - CONTROL-H f: Prompts for the name of a Lisp function and prints the documentation for it. Because commands are Lisp functions, you can use a command name with this command.

+   - CONTROL-H i: Takes you to the top menu of info, a documentation browser. Generally a complete info manual and emacs manual are on-line, and other GNU packages have manuals here too. The info utility has its own system help. Type ? for a summary or h for tutorial.

+   - CONTROL-H l (lowercase "ell"): Shows the last 100 characters typed. The record is kept after the first-stage keyboard translation. If you have customized the keyboard translation table, you must make a mental reverse translation.

+   - CONTROL-H m: Shows the documentation and special key bindings for the current Major mode (that is, Text, C, Fundamental, and so on).

+   - CONTROL-H n: Shows the emacs news file (new changes made to emacs, or ordered with most recent first).

+   - CONTROL-H t: Runs an emacs tutorial session. When you are finished with the tutorial, you can reselect your original buffer with CONTROL-x b or kill the buffer with CONTROL-x k (page 500).

+   - CONTROL-H v: Prompts for a Lisp variable name and gives the documentation for that variable.

+   - CONTROL-H w: Prompts for a command name and gives the key sequence, if any, bound to that command. Multiple key sequences are allowed. How-ever, for a long key sequence in which only the first part is recognized, the command describes the first part and quietly inserts the unrecognized part into your buffer. This can happen with three-character function keys (F1, F2, and so, on the keyboard) that generate character sequences, such as ESCAPE [SHIFT].

In this abbreviated presentation, it is clear that you can use the help system to browse through the emacs internal Lisp system. For the curious here is Stallman's suggested list of strings that match many names in the Lisp system: