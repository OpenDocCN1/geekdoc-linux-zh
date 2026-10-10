The fifth argument, on line 51, is the cursor. The mouse pointer changes to the cursor when the mouse is grabbed, and changes back again when it is released. Using a `NULL` pointer for the cursor causes the cursor to remain unchanged. Figure 12-2 shows the window with the cursor changed to a crosshair.

![](bbox=[0.11, 0.24, 0.26, 0.35])

**Figure 12-2: A grabbed mouse with a cursor change**

The last argument, on line 52, is the time that the grab is supposed to take place. As a convenience, the constant `GDK_CURRENT_TIME` automatically is converted to the current time, which is usually what you want.

There are two ways to get out of the grab. Pressing the “Ungrab” button executes the callback function ungrabMouse() on line 54. If the call to `gtk_pointer_grab()` returns `TRUE`, the mouse has been grabbed and should be released. The call to `gtk_pointer_ungrab()` releases the pointer. This program doesn’t allow the mouse to leave the window, so the mouse cannot close the window while the grab is in effect. However, it is still a good idea to release the grabbed mouse when a program exits. The function `eventDestroy()` on line 63 is called when the window is destroyed; so if the mouse has been grabbed, it is released by the call to `gtk_pointer_ungrab()` on line 66.

# ## Reading Characters from the Keyboard

Whenever you type something on the keyboard, the keystroke information goes to only one window; therefore, it all goes to one application. When a window is set to be the recipient of keyboard input, it is said to have the keyboard *focus*. There are a number of things that can happen to cause a window to receive the focus, but the most common is for the mouse to select the window. The title bar at the top of the window changes color on the window with the current focus.

Most of the time, you will want to use text input widgets to read information from the keyboard; but if you find that you need to read the keyboard directly, you can do it. You simply need to establish the correct set of callbacks. There are two basic kinds of keyboard events: one when a key is pressed and another when it is released. If you just want keystrokes, use the key press event. The key release event is necessary if you need to know whether a key is being held down.