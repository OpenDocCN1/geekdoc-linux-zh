
## Adjusting Keyboard Layout

You might need to adjust your keyboard's layout for any of a number of reasons. By keyboard layout, I don't mean the physical placement of the keys, but rather, what keys produce what actions. There are several reasons you might want to modify your keyboard's layout, including

- To gain access to keyboard features that are unique to your nation. Keyboards sold in Germany, for instance, have a slightly different mix of keys than do keyboards sold in the United States.
- To fix problems with keys that don't work as expected. For instance, word processors often use unusual key combinations, such as Shift+Tab, to perform functions. If whoever designed your default keyboard layout overlooked an important but unusual keystroke or mapped it incorrectly, you might need to adjust the layout to fix this problem.
- To create an unusual but desirable keyboard layout. For instance, some people prefer to use the Dvorak keyboard layout, which is optimized for better typing speed and less physical strain than is the more common QWERTY layout.

Unfortunately, adjusting your keyboard's layout entails different procedures for use in text mode than for use in X. You might therefore need to go through two parallel procedures rather than a single procedure to correct any keyboard problems you might have. It's also possible to configure Linux so that your keyboard works one way in text mode and another in X. This sort of configuration can be confusing and annoying—a keypress that works fine in a text-based program in an xterm in X might not work when you shut down X and work in text mode, for instance.

### Keyboard Mapping Theory

When you press a key on your keyboard, several things happen:

- The keyboard sends a *scan code* to the computer. The scan code is an unprocessed representation of the key that was pressed. Depending upon the type of keyboard in use (QWERTY versus Dvorak; United States versus German; and so on), the same scan code might correspond to a different function or symbol.
- Some applications operate in *scan code mode*, and work on the scan codes as delivered by the keyboard. The kernel delivers scan codes directly to these applications.
- Other applications work on *key codes*, which have been parsed by the kernel into uniform codes no matter what type of keyboard is attached.
- Most text-mode applications don’t work with either scan codes or key codes. These applications use codes that have been further parsed by Linux’s terminal driver. I refer to these codes as *terminal codes*. The terminal driver takes key codes and converts them into a form that’s uniform, not just across keyboards, but across widely varying input devices, such as Telnet sessions or console logins.
- X works on scan codes and processes those scan codes in a way that’s analogous to what happens for text-mode programs. In fact, text-mode programs run in an *xterm* window receive the same terminal codes they receive in text mode. Because the processing to get from scan codes to terminal codes is different, though, the keyboard mapping might be subtly—or wildly—different, as well.

It’s possible to modify the keyboard layout at any step in this process. The most common points are in the mapping from key codes to terminal codes and in X’s keyboard mapping from scan codes. Some keyboards are also programmable. If you have such a keyboard, you can reprogram it to produce a different set of scan codes. A few models, for instance, support remapping so that they produce the Dvorak layout natively.

## Text-Mode Keyboard Layout

The principal method of setting the mapping from key codes to terminal codes in text mode is to use the program `loadkeys`. This program loads the specified keyboard map file and instructs the kernel terminal driver to use it for keyboard input. Linux distributions normally include a call to `loadkeys` in a configuration file. For instance, in SuSE 6.3, the file `/etc/rc.d/init.d/kbd` contains this call. In Caldera OpenLinux 2.3, the equivalent call is made in `/etc/rc.d/init.d/keytable`. Other distributions might place this call in other locations.

The trick to modifying a key map is to change which key map `loadkeys` uses. In the United States, most users configure their systems at installation to call an appropriate U.S. keymap. This key map file is probably called us.map and is buried in an obscure directory such as `/usr/lib/kbd/keymaps/1386/qwerty`. Of course, the Linux installation program handled setting up the details of the mapping, so you were probably unaware of these details. To change the key map, I recommend you locate the script or configuration file that specifies the key map file, and then change that file. In Caldera OpenLinux 2.3, for instance, the `/etc/sysconfig/keyboard` file contains the name of the key map file. You can change this definition to another predefined file, or you can change it to a file you create yourself. You can then copy and modify a key map file that’s almost right.

A key map file consists of a series of lines like the following:

```
keycode 8 = seven          ampersand braceleft  Control_underscore
```

This line lists four meanings of the key code. Which meaning is used depends on which modifier keys are used (Shift, Ctrl, or Alt on most keyboards, with additional options for left and right variants of these). Each modifier key has a value, as shown in Table 15.1. Which key meaning is used depends upon the sum of the modifiers. For instance, with no modifiers, the value is 0, so it's the 0th field—seven in the preceding example. With the Shift key pressed, the value is 1, so the value is ampersand. The Ctrl+Shift combination yields a value of 5, so the 6th field would be used. The preceding line includes only four fields, so in practice, this combination can be handled by individual programs as they see fit. Because the modifiers go up to 128, it's possible to have a very long line in the key map file—up to 256 entries.

**TABLE 15.1 Modifier Keys Used in Key Map Files**

| Key | Value |
| --- | --- |
| Shift | 1 |
| AltGr | 2 |
| Ctrl | 4 |
| Alt | 8 |
| ShiftL | 16 |
| ShiftR | 32 |
| CtrlL | 64 |
| CtrlR | 128 |

AltGr refers to the right Alt key. Shift and Ctrl refer to either Shift or Ctrl key, respectively, whereas these names with L or R appended refer to the left or right keys only.

If you want to modify just one or two keys, you can do so without adjusting your entire key map. You can do this using the keycode command, which takes the form:

```
keycode n = function
```

You must know the key code number and the function name in order to use this command. You can find the key code generated by a key by using the showkey command. Type showkey and the program displays the key codes generated by any key press you make.

## X-Based Keyboard Layout

The principles of X keyboard layout adjustment are similar to those for text-based keyboard layouts, but some of the details differ. The basic keyboard layout selection is handled by the Keyboard section of your `XF86Config` file. This section should look something like this:

```text
    Section  "Keyboard"
    Protocol "Standard"
    XkbRules "xfree86"
    XkbModel "omnikey101"
    XkbLayout "us"
    XkbVariant "nodeadkeys"
    EndSection
```

This example sets the keyboard layout to use the `us` rules. You can change the layout by changing this code to another appropriate code, such as `de` for a German keyboard layout.

You can make adjustments to individual keys, or the entire mapping, by using the `xmodmap` command. To adjust an individual key’s meaning, you can use the `-e` parameter to bind a key code to an action, as in

```bash
xmodmap -e 'keycode 23 = Tab'
```

To adjust a group of key bindings, you can place assignments like the one inside the quotes in the preceding example, one per line, in a file. You can then pass that file to `xmodmap`, as in

```bash
xmodmap xmodmap-bindings.txt
```

> ### Tip
> Many distributions are configured to run `xmodmap` and pass it the `~/.Xmodmap` file when you log in. You can therefore place your adjustments in this file and not have to call `xmodmap` yourself.

Some Linux distributions configure the `Backspace` and `Delete` keys in a way that most individuals find confusing. You can alter their behavior by using the following `xmodmap` assignments:

```text
keycode 22 = BackSpace
keycode 107 = Delete
```

## Adjusting Key Repeat Rates

When you press a key, you get one instance of the associated character or action. If you keep the key held down, though, the computer begins repeating that key. By default, most Linux distributions set the key repeat rate to its maximum value, which is far too high for an average
