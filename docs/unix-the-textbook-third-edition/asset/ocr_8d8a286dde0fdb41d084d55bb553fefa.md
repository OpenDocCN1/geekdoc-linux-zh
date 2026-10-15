keyboard macro, in its current form, using that name. The macro name is an elisp symbol, and defining it in this way makes it a valid command name for invoking or using it with <Alt+X>, or for binding a key to it with global-set-key. If you specify a name that has a prior definition other than a keyboard macro, you get an error.

+   2. <Ctrl+X> <Ctrl+K> b <Enter> key <Enter>
+   
+   Binds the most recently defined keyboard macro to a key sequence (for the duration of the current emacs session only) (kmacro-bind-to-key).

+   3. <Alt+X> insert-kbd-macro <Enter> [macroname <Enter>]
+   
+   Inserts in the current buffer a keyboard macro's definition as elisp code. If you do not supply an already-defined macroname, the last keyboard macro defined is inserted as elisp code.

+   4. <Alt+X> macroname <Enter>
+   
+   Invokes macroname in the current buffer.

+   5. Pressing the function key <F4> invokes the last defined keyboard macro.

# 3.3.13.5.3 Saving Keyboard Macros for Future Sessions

Once a keyboard macro has a name, you can save its definition in a file, and particularly in the ~/.emacs file or other initialization file that you may use to initialize emacs at startup. By taking the following steps, it can be used in all future editing sessions.

The steps to accomplish this are as follows:

+   1. Visit the file you want to save the definition in, which becomes the current buffer. This is usually ~/.emacs.

+   2. Use the command <Alt+X> insert-kbd-macro <Enter> macroname <Enter>
+   
+   This uses the macroname you already have previously defined, and inserts equivalent elisp code that the keyboard macro represents, into the current buffer.

+   3. Save the current buffer. If the file you save in is your initialization file ~/.emacs, then the macro will be defined for all future sessions of emacs.

# 3.3.13.6 Redefining Keyboard Keys

This section describes key bindings, which map keys to commands, and keymaps, which record key bindings. It also explains how to customize key bindings, which is done by editing your init file.

# 3.3.13.5.4 Keys, Commands, and Variables

Emacs does not assign meanings to keys directly. Instead, emacs assigns meanings to named commands, and then gives keys their meanings by binding them to commands.