+   * `Ctrl-h m` Opens a window containing a description of all the currently active modes, including keybindings.
+   * `Ctrl-h k` A prompting help key. After pressing this combination, you are asked (in the minibuffer) to press the key or key sequence for which you need help. A window opens, describing just what the key does.
+   * `Ctrl-h a` Another prompting key, this one is known as apropos help. When prompted, type a word, function name, or variable name. A window displays all the Emacs commands containing the word or name. This is a good way to find commands when you don’t know the exact name.
+   * `Ctrl-h f` Prompts you for a Lisp function name and then shows the documentation in a window. Since Lisp commands are functions, you can also type a command name.
+   * `Ctrl-h t` Starts the Emacs tutorial, a short introduction to Emacs for the first-time user.
+   * `Ctrl-h v` Shows you a variable’s value. This is a quick way to see what default settings are in use.
+   * `Ctrl-h I` Brings up the Info help file browser, which is covered in Chapter 15, “External Convenience Packages.”

# ### Loading and Saving Files

You will use the following commands constantly, which makes them perfect candidates for re binding to a single keystroke, such as one of the function keys (see Chapter 10 for keybinding instructions). Except for the buffer-saving command, these commands prompt you for a file name in the minibuffer. Here are the default keybindings:

+   * `Ctrl-x Ctrl-f` Loads a new file. Think of the "f" as standing for "find a file."
+   * `Ctrl-x k` Kills a buffer; if you have unsaved changes you will be asked if you want to save the buffer.
+   * `Ctrl-x Ctrl-v` Replaces a file you just loaded with another one. This can be thought of as a combination of the above two commands.
+   * `Ctrl-x i` Prompts you in the minibuffer for a file name. The contents of the file specified are then inserted at the point position.
+   * `Ctrl-x Ctrl-s` Saves the current state of the buffer to disk, overwriting the original file.