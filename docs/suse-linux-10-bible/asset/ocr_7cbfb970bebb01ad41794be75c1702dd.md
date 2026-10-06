By default, the vim editor is installed (vi improved). It adds extra functionality
the traditional vi text editor.

One of the first things that may stump you when you first start using vi is the fact
at you cannot enter any text when you just type vi at the command line. This is
t reason that a lot of people do not like vi and move to emacs. However,
before you move on, let us explain what's happening: vi/vim uses a command mode
a text mode. In command mode, you can manipulate the text with commands,
save and quit files, and open files without "entering" text into your document. You
actually edit text with the traditional methods (insert, delete, and so on), you need
to move out of command mode.

This may seem quite alien at first, but we hope that with some examples you will see
that it is a quite powerful way to do things, and for people who work more quickly on
the command line, it can dramatically speed up your text-editing needs.

Figure 11 is what you will see when you type vi or vim at the command prompt.
as soon as vim has loaded, it is automatically in command mode. To move into
insert mode, press the i key. If you want to insert a new line at the current position,
use the o key. This inserts a new line and puts you in insert mode.

![](bbox=[0.181, 0.507, 0.857, 0.866])

Figure 11-1: Loading vim