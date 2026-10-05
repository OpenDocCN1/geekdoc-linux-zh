In practice, unfortunately, the assignment of user-defined keyboard shortcuts is not as easy as it might look:

+   * GNU Emacs and Emacs have different syntax for composite keyboard shortcuts. In GNU Emacs, `Ctrl-X` is represented as `[C-x]`; in Emacs, in contrast, as `control x`.

+   * The default meaning of some keyboard shortcuts changes with nearly every Emacs version. (Particularly prone to thay you found a reasonable configuration, are `Del` and `Backspace`. As soon as you thought the next version comes and voids all your efforts ...)

+   * The code X server usually supplies to Emacs when you press a key combination depends highly on the X configuration (particular on `xodmap`). That `Del` may behave differently in two Linux distributions, even with identical Emacs configuration!

+   * Some keys are claimed by Linux, the X server or the window manager and are no longer available for use in Emacs (for example, `Ctrl-Alt-F7` to switch between consoles).

+   * When Emacs is used in a text console, many keyboard shortcuts cannot be processed at all. Furthermore, the meaning of the keyboard shortcuts also depends on the `loadkeys` program.(Keyboard shortcuts in consoles will be treated further in this context. This chapter assumes that you are using Emacs under X.)

+   * Finally, several Emacs restrictions must be observed: many keyboard shortcuts are preassigned, and it does not always make sense to substitute these shortcuts with one's own shortcuts. Some keys activate a separate level of shortcuts and can only be used in combination with additional keys (for example, `Ctrl-X`, `Ctrl-C`, `Ctrl-H`).

For all reasons it is completely impossible to write a `.emacs` file that really works in the same way on every computer.

In order to find out how Emacs reacts to a key press, you can use the key combination `Ctrl-H C` key. Emacs displays the internal character of the string pressed plus the current meaning of that keyboard shortcut. For example, `Ctrl-H-C-F5` leads to the message `is is undefined`.

`Ctrl-H-C` is also a good way to determine the Emacs-internal symbol for special keys. `Ctrl-H-C-Home`, for example, yields `home runs...`. Thus you know that `Home` is represented by `Chome1`.

![](bbox=[0.115, 0.693, 0.137, 0.783])

# GNU Emacs syntax for keyboard shortcuts

The entire shortcut is placed in square brackets. Inside the brackets, either single characters (preceded by ?) or keywords for function keys (without ?) can be specified.