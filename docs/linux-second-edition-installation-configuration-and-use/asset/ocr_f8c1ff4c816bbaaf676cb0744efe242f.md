# BUFFERS AND WINDOWS 557

Replace function(\[^,]*\, \[\^,]*\*) with function(\2,1); at each occurrence of function, the two parameters are exchanged. Enchanged, function(a+b,2) becomes function(2*a,b). The only condition is that there must be no commas in the parameters of the function. When trying to exchange the parameters in function(f(a,b),g(x,y)), the command failed.

Please be careful when you use the pattern search and replace command and save your first text. Especially during when the pattern search finds different (and often much larger) texts you had planned. (With Ctrl+Z (that is, use Ctrl+Shift+Z) you can undo an erroneous replace command step by step.)

# Keyboard shortcuts for processing the found text

+   - Spacebar: continue search
- replace, but leave cursor where it is (in order to be able to check the result; when the command can be continued with Spacebar)
- ← or N: do not replace, continue search
- Esc: do not replace, abort command
- ! carry out all further replacements without requests for confirmation (caution!)
- Ctrl+R: interrupt the command to carry out a manual correction at the cursor position (recursive edit)
- Ctrl+Alt+R: resume the command

# # 16.9 Buffers and windows

You can use Emacs to edit several texts at a time. Each text is managed in a so-called buffer. Even when you work on a single text, several buffers exist: one for the text (the buffer name corresponds to the file name (without path)), one for Info or help window opened at some time during work (buffer names *info* or *help*), one for the most recently displayed list of commands expanded with Tab (*completions*), for the abbreviations (*abbrevs*, if some time Alt+X edit-buffers has been executed; see below), and so on.

Besides the concept of buffers, Emacs also has windows: a window is an area on screen in which a buffer is displayed.

Normally, a single window is used which takes all available space. For the execution of some commands (for example, the display of help or other Emacs-internal information) the screen is horizontally split into two windows. The screen can also be divided into several horizontal or vertical strips. In each of these areas (windows) a different buffer can be displayed. You can also display the same buffer in two different windows. (This is mainly useful for very long texts: you can work