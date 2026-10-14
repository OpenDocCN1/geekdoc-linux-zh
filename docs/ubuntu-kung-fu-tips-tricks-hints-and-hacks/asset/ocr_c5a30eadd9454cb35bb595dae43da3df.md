of the oldest command-line programs for Unix. Most people agree that bash offers the best all-round mix of functionality and ease-of-use.

Command-line programs are sometimes known as shells, and the term comes from the fact that—like mollusks and crustaceans—the shell “wraps around” the delicate interior of the operating system, protecting it from accidental damage!

> NOTE A graphical user interface is sometimes referred to as a shell because, by the above definition, it has the same function as a command-line prompt.

Other shell programs are sometimes used under Linux instead of bash. Perhaps the most popular are Korn Shell (ksh) and C Shell (csh). Both are geared towards programming and it’s unlikely you’ll ever come into contact with them. bash is the default in most popular Linux distros.

# To DOS or not to DOS

You might be wondering if the Linux command-line is similar to Microsoft DOS. They’re distant cousins rather than siblings. DOS was a clone of CP/M, that itself borrowed much from the Unix command-line. Some DOS knowledge will give you a head start, but you will have to unlearn as much as you learn!

# Understanding the prompt

Let’s get stuck-in straight away.

# Starting a command-line session

There are two ways to start a command-line session: by running a desktop terminal program (sometimes known as a terminal emulator), or by switching to a virtual console (also known as a virtual terminal). In both cases you’re accessing exactly the same command-line.

To switch to a virtual console, hit Ctrl+Alt+F2. The GUI will disappear and be replaced by a login prompt. Don’t worry—your desktop is still there, and you can switch back to it by hitting Ctrl+Alt+F7. It’s just that the virtual console needs to take over the screen.

> NOTE There are six virtual consoles, and they’re accessed by hitting Ctrl+Alt and F2, F3, F4, F5, F6. The console on F1 is used for debug and log output, so is best avoided.

Login by typing your username, and then the password. You won’t be prevented from logging in because you’re already logged in at the desktop—under Linux a user can login as many times as she wants.