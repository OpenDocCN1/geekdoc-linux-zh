If you spend some time tweaking the ispell and/or Flyspell settings, you should be able to come up with a level of spell-checking activity that is effective and unobtrusive.

# # Running a Shell in Emacs

Emacs has its own shell mode, a window that is similar to a login shell session in an xterm or at a virtual console. Your familiar shell, whether it is bash, tesh, zsh, or any other command shell, is used with the same startup scripts as in any login session.

To open a shell buffer, just press M-x and type
shell

You can run other command-line programs from this shell buffer as long as they don't manipulate the display. ncurses-based programs won't work. Any of the GNU file and text utilities such as ls or cat are good examples of programs that output nothing but text and thus are appropriate. Programs run from a shell buffer run asynchronously, which means that they are running in a process outside of Emacs and don't affect the editor's behavior.

So why would you bother, when xterm or rxvt windows are a dime a dozen and don't have the limitations of the shell buffer? One (the only?) reason is that the output of a command in the shell buffer can be manipulated like text in any other Emacs buffer. You can copy the text and paste it into another buffer. Probably programmers are the main users of the shell buffer these days. The GNU gcc compiler is used by a great majority of free software developers, and its output (especially error messages) can be useful in an Emacs session.

Consider also that the Emacs shell buffer was developed in an era of slow, resource-hungry computers; in those arcade times, it was a truly useful and good concept. Nonetheless, even with today's powerful and memory-rich machines, the Emacs shell buffer can still be worth using.

# ## Shell Buffer Keybindings

You might have become accustomed to the usual shell keybindings, but the Emacs Shell buffer bindings are different.

In most Linux shells, the previous commands are kept in memory; and you can bring one back in order to run it again by pressing either the up-arrow key or M-p. The Emacs shell buffer supports only the latter binding. Tab file name completion works, but some of the bindings for process manipulation are different in the Shell buffer. In a normal shell session, pressing Ctrl-c interrupts a running process. That