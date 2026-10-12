After you press Enter, you will be prompted for the root password. Enter the password and click OK. You will then see the Keyboard dialog box shown in Figure 4.2. This dialog box is similar to that displayed by `system-config-keyboard`.

![](bbox=[0.32, 0.17, 0.71, 0.44])

**FIGURE 4.2** The `system-config-keyboard` client is used during an X session to choose the language you will be keyboarding in during your desktop sessions.

Scroll through the list of languages, highlight a language, and then click OK to save your change. Table 4.1 lists text-based and graphical commands you can use to manipulate or get information about your keyboard.

TABLE 4.1 Linux and X Keyboard-Related Commands
| Command | Description |
| :--- | :--- |
| dumperkeys | Displays keyboard translation tables |
| kbd_mode | Modifies current keyboard mode |
| kbrate | Changes keypress delay, repeats |
| loadkeys | Loads new keyboard table |
| showkey | Prints character, keycode, and other keystroke information |
| setleds | Displays, changes keyboard light-emitting diode (LED) settings |
| xkbopt | Shows, sets keyboard character translations for X |
| xkbprint | Displays or saves X keyboard mappings |
| xset | Modifies keyboard settings for X |
| xmodmap | Changes key mappings for X |

The X11 keyboard and other clients can be used to input a keyboard description into a running X server, show current keyboard character translations, change a keyboard map, and set other keyboard (and pointer) preferences. X11 settings are generally contained in a system's `xorg.conf` file (see Chapter 6, "The X Window System," for more information).