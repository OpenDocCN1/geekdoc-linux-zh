![](bbox=[0.26, 0.09, 0.7, 0.33])

FIGURE 4.2 The system-config-keyboard client is used during an X session to choose the language you will be keyboarding in during your desktop sessions.

Scroll through the list of languages, highlight a language, and then click OK to save your change.

Table 4.1 lists text-based and graphical commands you can use to manipulate or get information about your keyboard.

TABLE 4.1 Linux and X Keyboard-Related Commands |  |  | |dumpeys | Displays keyboard translation tables | |kbdmode | Modifies current keyboard mode | |kbd rate | Changes keypress delay, repeats | |loadkeys | Loads new keyboard table | |showkey | Prints character, keycode, and other keystroke information | |setleds | Displays, changes keyboard light-emitting diode (LED) settings | |xkbcomp | Shows, sets keyboard character translations for X | |xkprint | Displays or saves X keyboard mappings | |xset | Modifies keyboard settings for X | |xmodmap | Changes key mappings for X |

The X11 keyboard and other clients can be used to input a keyboard description into a running X server, show current keyboard character translations, change a keyboard map, and set other keyboard (and pointer) preferences. X11 settings are generally contained in a system’s xorg.conf file (see Chapter 6, “The X Window System,” for more information).

As a trivial example, the following short shell script (see Chapter 14 for more information on how to use shell scripts) can be used to blink the keyboard Caps Lock LED on and off each second (press Ctrl+C to stop the blinking) while using the console: