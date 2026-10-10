
When you place the pointer in or on windows or other objects, pressing the left button activates the window or object. Pressing the right button or pressing the middle button—or, on a two-button mouse, pressing both the left and right buttons simultaneously—will also cause certain actions to take place, such as the appearance of a menu from which you can select further actions.

In X, the location cursor is similar to the cursor on the command line of your character-based screen. Its location determines where to insert your keyboard input on a terminal emulation screen. The location cursor is not activated until you activate the terminal window first, however.

## Window Frame

The frame around a window is often taken for granted. Although we generally think of the window contents and frame as one and the same, they are not. Strictly speaking, the frame is provided by the window manager application and enables a certain amount of window manipulation without affecting the operation of the application running in the window itself. That window manipulation, however, requires the proper placement and operation of the mouse. The basic components of the window frame might vary slightly from one window manager application to another (for example, one might have an exit button at the far right end of the title bar, but another might not).

The first component of the window frame is the title bar, which runs across the top of the window between the window operations button on the left and the minimize and maximize buttons on the right. Predictably, the title bar contains the title of the window. For instance, the window emulating a terminal screen would be titled xterm. You can use the title bar to move the window from place to place on the root menu by the drag-and-drop method.

NOTE: The term “drag and drop” refers to the following actions: positioning the mouse cursor over something (such as a title bar or menu option) and pressing but not releasing the left mouse button; then moving the mouse cursor to another location (dragging) and releasing the left mouse button (dropping).

You can reduce the window to its icon representation (its minimum size) by left-clicking the minimize button, which is immediately to the right of the title bar. If the window is smaller than its maximum size, you can maximize it by left-clicking the maximize button next to the minimize button (maximum size usually means that the window will fill the entire root window). Some window managers also provide an *exit* or *close* button, which usually looks like a square with an X in its center, in the upper-right corner of the window frame. Left-clicking that button will close the window, the same as left-clicking the window operations button and selecting the *close/exit* option.

Speaking of resizing the window, there are several ways of making the window larger or smaller. All require proper placement of the mouse pointer. Note that if you place the pointer exactly in the corners of the window frame, the pointer changes to resemble something like an arrow pushing against the corner. By dragging and dropping at that point, you can alter the window's dimensions in two directions (height and width) simultaneously, if you want.

If you just place the mouse on any of the four borders (top, bottom, left, or right) of the window frame at any one time, the pointer again changes, but this time it changes to something resembling an arrow pushing against that border only. Now you can drag and drop again, but you can change only one window dimension at a time.

If you move the mouse pointer to the upper-left corner of the window frame and left-click on what is called the *window operations button*, you will activate a drop-down menu containing several commands. You can move the pointer down the menu and select the operations of your choice.

## Icons

You probably already know about the benefits of icons on your desktop. They are a handy way of multitasking without repeatedly having to invoke applications, and they are a handy way to manage your root window (that is, *desktop*) space. When an application window has been changed to an *icon*, the process remains invoked and ready, but the screen clutter is reduced.

You can create an icon from an active application in two ways. One is by left-clicking the window operations button in the top-left corner of the application window and then scrolling down the resulting drop-down menu to select the minimize (or *hide/restore* or similar instruction) option. The benefit of using this method stems mainly from having a choice of options presented to you. The result is the same as the second and simpler method, namely left-clicking the minimize button on the window frame.

Depending on the window manager used, the resulting icons for identical applications might be different in appearance. For example, minimizing the calculator window in `fwm95` results in an icon that looks like a button bar. Minimizing the same window in `lesstif` results in an icon that looks like a reduced-scale calculator. No matter which window manager you use, the resulting icons are actually bitmap images.

## xterm Fundamentals

An xterm window is an X client application that simulates a common video terminal, such as a DEC vt100. By now, you have undoubtedly noticed that you can create and use xterm windows (commonly called xterm, AiXterm, or something similar, depending on the version of UNIX) while in X to enter Linux/UNIX commands in the same manner you entered them at the command line when X was not invoked.

### Create an xterm Window

You can create additional windows in X in two ways. First, from an already opened xterm window, you can type `xterm &`. Alternatively, you can move the mouse pointer to an open area of the desktop (that is, the area not already occupied by a window) and left-click the mouse. Then, from the resulting root menu, left-click New shell, which is the first selection under Start at the top of the root menu.

### Copy Text

The xterm window enables you to copy and paste text to another part of the window or to another window. Place the mouse pointer at the first letter of the text you want to copy, and then left-click and drag over all the text you want to copy. The text is highlighted. When you release the mouse button, the highlighted text is copied into a buffer. Then, you move the mouse pointer to a position in the same window or in another xterm window. If you are using a three-button mouse, press the center button to copy the text. If you are using a two-button mouse, push both buttons at once.

### Create a Scrollbar

If you want to create a window with a scrollbar in it, first create another preliminary window. In that preliminary window, type one of the following command sequences:

```
$ xterm -sb leftbar<Enter>
```

or

```
$ xterm -sb rightbar <Enter>
```

Each of these sequences creates a new window with a scrollbar on the side that you specify.

If you want to create a scrollbar in an existing window, place the mouse pointer inside that window, hold down the Ctrl key, and press the center button on the mouse (on a three-button mouse) or press both mouse buttons at once (on a two-button mouse). The VT Options menu is displayed on the screen. The first, or one of the first, selections on the menu is Enable scrollbar. Click that selection, and a scrollbar appears in your window.

To use the scrollbar, place the mouse pointer in the scrollbar itself and then press the left mouse button to move up or press the right mouse button to move down. If you want to remove the scrollbar, redo the instruction and left-click Enable scrollbar to remove the check mark next to that selection.

Use the man pages, the help options, and other information sources to see what else you can do with the `xterm` command.

### Close an xterm Window

To close an xterm window, you have several alternatives. At the prompt in the window, press Ctrl-D or type `exit` and press Enter. Double-click the Window-Ops button in the upper-left corner of the window or left-click that same Window-Ops button and then left-click **Close** on the resulting drop-down menu.

### Customize xterm

We have already discussed a couple of xterm options:

- Running the second xterm window in the background so that you can move back and forth from window to window (the & option)
- Adding a scrollbar to the new xterm window (using the -sb option with either the -leftbar or -rightbar option)

In this section, we present a few more of the dozens of options available to you with the xterm command. Combining these options gives you perhaps thousands of possibilities for new xterm windows. Take a look at Example 14.1 and Table 14.4 to see how xterm can work for you.
