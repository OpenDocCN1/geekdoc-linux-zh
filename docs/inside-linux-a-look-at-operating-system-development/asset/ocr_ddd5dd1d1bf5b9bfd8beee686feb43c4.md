Although shell scripts generally read a line at a time, other programs have a mechanism to read each character as it is entered—called raw mode. The pre-processing is quite useful when entering shell commands or text, but editors and the like would just as soon not require the user to press <ENTER> after each command—especially considering many of the commands consist of a single keystroke.

# ### 3.2 Graphical User Interface

There exist menu-based tools, such as curses, which can paint the screen with arbitrary mapping of characters and allow the user to move a box cursor about to select options, but this is regarded as passé.

Almost all computer systems sold today have some kind of pixel addressable display (usually in color) and a pointing device such as a mouse. These displays support a graphical user interface (abbreviated GUI and pronounced "goopy") which presents icons which can be clicked on to select options or execute programs. The practice is to "click, double-click, or drag-and-drop" to cause things to happen.

Linux uses the X Window System, also called X-Windows or just X, to provide such a graphical interface. X is the system of choice for all of the most powerful systems and it is now available on the personal computer. X was an outcome of Project Athena at MIT sponsored by DEC and IBM. They were joined by other industry leaders—including Hewlett-Packard, Sun Microsystems, and AT&T—in forming a consortium which provides sponsorship for continuing development.

X relies on what many regard as an unusual twist to the client/server model—the display, keyboard, and mouse are under the control of what is called a server and the client is an application program somewhere on the net. This model has confused a great number of people because they draw an incorrect analogy with the networked file system client/server model. They think they, not their programs, are the client. Thus they think X is backwards. If they were to realize that their program is the client, the client/server model is entirely consistent.

This network based client/server model has led to one interesting outcome—the development of X terminals. These are small computer systems with a processor, a keyboard, a bit-mapped display, a network