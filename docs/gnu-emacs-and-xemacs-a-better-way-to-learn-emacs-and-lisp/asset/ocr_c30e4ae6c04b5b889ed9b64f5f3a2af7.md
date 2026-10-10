You will be prompted for a name. This should be a name unused by any Emacs variable, command, or function. There is a custom in the Emacs community of prefixing personal macros, functions, and variables with your initials. This ensures that the names won't conflict with other Emacs names and gives an added benefit: you can view the names of all personal macros, etc. by using the Apropos help key along with your initials and using Tab completion to bring up the list.

Now that your macro has a name, you can execute it as you would any other minibuffer command. Press `M-x` and type `macro name`.

Now that you have a named macro, you can save it to a file. If you plan on using the macro infrequently, the file could be a Lisp file that would need to be explicitly loaded when needed. Perhaps the macro will be used only in a particular directory. In this case, the file containing a macro or macros can be loaded automatically through a notation in the files in that directory. Lines such as these at the end of a file inform Emacsthat you would like the macro file loaded whenever the file is loaded:

```
Local Variables:
eval: (load-file "my-macros.el")
End:
```

Any macros that you anticipate using often can be inserted directly into your ~/.emacs file.

Writing the macro to a file is not difficult or involved. If you want a named macro written to a file, first load the file. Position the cursor at the desired location in the file, press `M-x,` and type `insert-kbd-macro`

You will be prompted for the macro's name. Type it in the minibuffer and press Enter. Lisp code representing your macro will appear in the file.

Remember the "mytime" macro I described earlier? Here is what it looks like written by the preceding command into a file:

```
(defalias 'mytime (read-kbd-macro
"C-u M-! date SPC \*\!\!\&M SPC %p" RET 9*\<right> SPC RET>))
```

This is Lisp code. Even if you don't know Lisp, you can get the general idea of what this code is doing.

Defining new keybindings for commands is discussed in detail in Chapter 10. For now, I'll just show how the preceding macro can be given its own keybinding in an .emacs file:

```
global-set-key [[control c] m] 'mytime)
```