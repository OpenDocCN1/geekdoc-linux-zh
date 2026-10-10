with various programs simultaneously.

+   Ease of control: to run most commands, they use a key combination — the so-called *command prefix* or *command key* — followed by another character.

+   Sessions can be detached from their current terminal (that is, programs are sent to the background and continue to run). This guarantees complete execution of programs no matter if we accidentally close a terminal, experience an occasional terminal freeze or even remote connection loss.

+   Socket connection.

+   Copy mode.

+   They are highly customizable.

# ## GNU Screen

In the earlier days of Unix (1970s - 80s) computers basically consisted of terminals connected to a central computer. That was all, no multiple windows or tabs. And that was the reason behind the creation of GNU Screen in 1987: emulate multiple independent *VT100 screens* on a single physical terminal.

# ### Windows

GNU Screen is invoked just by typing `screen` into the terminal. You will first see a welcome message:

```
```
GNU Screen version 4.05.00 (GNU) 10-Dec-16

Copyright (c) 2010 Juergen Weigert, Sadrul Habib Chowdhury
Copyright (c) 2008, 2009 Juergen Weigert, Michael Schroeder, Micah Cowan, Sadrul Habib Chowdhury
Copyright (c) 1993-2002, 2003, 2005, 2006, 2007 Juergen Weigert, Michael Schroeder
Copyright (c) 1987 Oliver Laumann
(...)
```
```

Press Space or Enter to close the message and you will be shown a command prompt:

```
```
$ 
```
```

It may seem nothing has happened but the fact is that `screen` has already created and managing its first session and window. Screen’s command prefix is `Ctrl` + `a`. To see all windows at the bottom