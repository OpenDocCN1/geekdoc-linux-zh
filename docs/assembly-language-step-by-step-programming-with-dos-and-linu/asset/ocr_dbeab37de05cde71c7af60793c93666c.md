buffer a name and save it to a disk file as a record of the make session.
It does the same when you invoke the GNU debugger from inside
EMACS: gdb's output is piped into a buffer, which you can save to disk
if you choose to for later reference.

Mostfully, you can invoke a Unix shell (i use bash) from inside
EMACS, and EMACS will pipe its output into a new buffer, which like
buffer can be saved to disk. Especially while you're learning,
there's very little that you'll need to do that can't be done either from
the EMACS menus or from a shell opened from within EMACS.

# Opening a Shell from inside EMACS

This is last worth explaining, because it is less obvious than most of
the editing commands. There is currently no EMACS menu item that opens
shell in a window. (There should be!) To open a shell, the command is
"Esc shell." You press the Esc followed by the lowercase x key
(don't press both at once!) and, in its command line at the bottom of its
window, EMACS will display the unhelpful string "M-x." This is its
way of expressing the sequence x on a PC. (The M stands for
"Meta," which was the name of a control key on some ancient and
cfully forgotten dumb terminal.) On other computers or
terminals that may lack an Esc key, there may be other ways of initi-
ing the command. EMACS was written to be portable. After the string
"M-x" you must type "shell" and press Enter.

EMACS will open a new buffer in a window and will begin piping shell
output from the default shell into that window. At the top of the window
will be your familiar shell prompt, waiting for you to type shell-
executables just as you did before you invoked EMACS. You can invoke the
utables you build by naming them (usually preceded by
".//") just as you would from the shell.

Note that you can exit the shell by typing "exit," but the window and
buffer that EMACS opened for the shell will not go away by themselves.
You have to kill the buffer as a separate operation, using the Files | Kill
nCurrent Buffer menu item.

I mentioned it earlier, but keep in mind that you can launch the GNU
Debugger by selecting the EMACS menu item Tools | Debugger.