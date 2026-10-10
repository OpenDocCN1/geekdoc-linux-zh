the key with that scancode has been pressed. Actually, `KEY_PRESSED` is 1 and `KEY_NOT_PRESSED` is 0, which allows you to use constructs such as this:

```
```
if (buffer[SCANCODE_ENTER]) {
    /* do something */
}
```
```

This is more efficient than calling `keyboard_keypressed()`, in case you want to check for many different keys. Note that keyboard events will only be processed when you occasionally call `keyboard_update()` or `keyboard_waitforupdate()`.

# ### void keyboard_clearstate(void)

When in raw keyboard mode, SVGLib receives press and release events from the kernel and keeps track of which keys are currently pressed. Calling `keyboard_clearstate()` sets this information to all keys released. You can use this for cleanup at certain places in your program. In addition, SVGLib resets the states of all keys when a VC switch occurs because it doesn’t know the current state of keys when it regains control of the console.

```
```
typedef void (*_keyboard_handler) (int scancode, int press); void
keyboard_seteventhandler(_keyboard_handler handler)
```
```

See `keyboard_setdefaulteventhandler()`.

# ### void keyboard_setdefaulteventhandler(void)

These functions allow you to define a keyboard event handler that is called by `keyboard_update()` and `keyboard_waitforupdate()` when a keyboard event occurs. The argument `press` is `KEY_EVENTRELEASE` or `KEY_EVENTPRESS` if the key scancode was released or pressed. Actually, the first value is 0, and the second is 1 (which are intuitive so that you may use them in your programs). Even if you specify your own handler, SVGLib will check for Alt+F** or Ctrl+C for console switches or generation of SIGINT, if allowed by `keyboard_translatekeys()`,

Calling `keyboard_setdefaulteventhandler()` reinstates the default handler, which maintains the tables used by `keyboard_getstate()` and `keyboard_keypressed()`. It’s probably a good idea to call `keyboard_clearstate()` after re-enabling the default handler. See `keyboard_keypressed()` for the list of scancodes.

# ## Joystick Handling

The functions in this section cover joystick handling:

> **Note**
> *These functions must include `<vgajoystick.h>`. The joystick module is basically independent from the rest of SVGLib. You can easily use it in text mode only, but there’s no benefit to doing that. If used in a graphics mode, however, it will release*