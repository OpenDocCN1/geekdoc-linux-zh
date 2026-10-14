⇒ Here are two ways to do this.

+   - To start GNU Emacs at a shell prompt, type:
+   
+     `$ emacs` ⏎
+   
+   - To start XEmacs at a shell prompt, opening a file named `journal`, type:
+   
+     `$ xemacs journal` ⏎

Upon startup in X, a typical GNU Emacs window looks like Figure 10-1 (the client window will differ depending on your window manager):

![](bbox=[0.255, 0.351, 0.687, 0.642])

*Figure 10-1. Emacs upon startup.*

The welcome message appears when Emacs first starts, and it tells you, among other things, how to run a tutorial (which we’ll look at in just a minute). The bar running along the entire left-hand side of the window is called the *scroll bar*. The X client window in which an Emacs session is displayed (or the terminal screen, when not running in an X window) is called the *frame*. Notice that there is no border along the sides (if you look closely, you can see that even the side with the scroll bar is lacking a border); that is because many of today’s window managers, including the one in the illustration, only draw borders on the top and bottom sides of a window.

The top bar is called the *menu bar*, and you can pull down its menus with the mouse by left-clicking a menu and then dragging it down. When you run Emacs in a terminal, you can’t use the mouse to pull down the menus, but