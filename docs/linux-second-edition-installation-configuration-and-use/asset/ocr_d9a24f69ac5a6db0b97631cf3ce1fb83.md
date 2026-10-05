# FUNDAMENTALS 543

In the Emacs documentation, keyboard shortcuts are represented slightly differently; DEL does not mean Del, but C stands for Control (meaning Ctrl and M for Meta.)

On most keyboards there is no direct correspondence for the Meta key. Instead of Meta+X, you must press Esc and X (one after the other). Alternatively, in some cases, you may use Alt+X (simultaneously) as well. In this book, we generally indicate the easier Alt key combination.

In some Emacs-compatible programs or when using Emacs in a text console, problems arise with the Alt key. Here, instead of Alt+X, you must employ Esc. Information about keyboard installation and Emacs configuration via the .emacs file can be found on page 17 from page 569.

Please note that Emacs differentiates between Ctrl+X, Ctrl+B and the very similar combination Ctrl+X, B. Thus, it really matters how long you keep the Ctrl key depressed.

# Mouse support

You will not be particularly surprised to know that you can use the mouse to change the position, select and copy text. (The usual X conventions apply, that previously selected text is inserted with the mouse button.) If you are displaying several texts at a time, you can also move the separation bar between the text areas by means of the mouse button.

Somewhat confusing is the handling of the scroll bar: in GNU Emacs it can, as in xterm, only be moved with the middle mouse button, whereas in XEacs, the left mouse button can be used as well.

Further mouse functions depend on the Emacs version. In XEacs, a position-dependent context menu appears when the right mouse button is pressed. (Try out the right mouse button in different areas of the status line!) In GNU Emacs, in contrast, you can use Shift and Ctrl in combination with the mouse buttons to execute various commands.

# X-specific options and resources

When starting Emacs under X, you can perform numerous setting for colors, charset set, and so on, by means of command line options. The following table lists the most important options. A complete description can be found in the manual page for Emacs.

| Command line options |
|---||
| -nw | start standard Emacs in the shell window (not the X variation in a separate window) |
| -fg color | foreground color (text color; default: black) |