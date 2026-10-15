# TABLE 3.18 emacs Summary

# Emacs Commands

| Command | Action |
|---|---|
| <Ctrl+X><Ctrl+F> | Visit a file (find-file) |
| <Ctrl+X><Ctrl+R> | Visit a file for viewing, without allowing changes to it (find-file-read-only) |
| <Ctrl+X><Ctrl+V> | Visit a different file instead of the one visited last (find-alternate-file) |
| <Ctrl+X><Ctrl+S> | Save the current buffer to its file (save-buffer) |
| <Ctrl+X> s | Save any or all buffers to their files (save-some-buffers) |
| <Alt+> | Forget that the current buffer has been changed (not-modified) |
| <Ctrl+X><Ctrl+W> | Save the current buffer with a specified file name (write-file) |
| <Ctrl+H> | Display a help message about these options |
| <Ctrl+X><Ctrl+C> | Exits emacs |
| <Ctrl+X><Ctrl+Z> | Suspends emacs and exits to the shell |
| Emacs Help Command | |
| <Ctrl+H> a topics <Enter> | Display a list of commands whose names match topics (apropos-command). |
| <Ctrl+H> b | Display all active key bindings—minor mode bindings first, then those of the major mode, then global bindings (describe-bindings). |
| <Ctrl+H> c key | Show the name of the command that the key sequence key is bound to (describe-key-briefly). Here c stands for "character." For more extensive information on key, use <Ctrl+H> k. |
| <Ctrl+H> d topics <Enter> | Display the commands and variables whose documentation matches topics (apropos-documentation). |
| <Ctrl+H> e | Display the *Messages* buffer (view-echo-area-messages). |
| <Ctrl+H> f function <Enter> | Display documentation on the Lisp function named function (describe-function). Since commands are Lisp functions, this works for commands too. |
| <Ctrl+H> r | Display the emacs manual in Info (info-emacs-manual). |
| <Ctrl+H> s | Display the contents of the current syntax table (describe-syntax). The syntax table says which characters are opening delimiters, which are parts of words, and so on. |
| <Ctrl+H> t | Enter the emacs interactive tutorial (help-with-tutorial). |
| <Ctrl+H> K key | Enter Info and go to the node that documents the key sequence key (Info-goto-emacs-key-command-node). |
| <Ctrl+H> | Display the help message for a special text area, if the point is in one (display-local-help). (These include, for example, links in "Help" buffers.) |