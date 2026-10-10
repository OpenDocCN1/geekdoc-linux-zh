# OPTIONS

For boolean options (**on** or **off**), the default is **on**.

Below, an *8-color* can be **black**, **red**, **green**, **yellow**, **blue**, **magenta**, **cyan**, or **white**.

A *16-color* can be an *8-color*, or **grey**, or **bright** followed by **red**, **green**, **yellow**, **blue**, **magenta**, **cyan**, or **white**.

The various color options may be set independently, at least on virtual consoles, though the results of setting multiple modes (for example, —**underline** and —**half-bright**) are hardware-dependent.

+   —**apcursorkies** [*on**/*off*] (virtual consoles only)
+   Sets Cursor Key Application Mode on or off. When on, ESC O A, ESC O B, etc. will be sent for the cursor keys instead of ESC [ A, ESC [ B, etc. See the *vi and Cursor-Keys* section of the *Text-Terminal-HOWTO* for how this can cause problems for *vi* users.

+   —**append** [*console_nuer*]
+   Like —**dump**, but appends to the snapshot file instead of overwriting it. Only works if no —**dump** options are given.

+   —**background** [*8-color*/*default*]
+   Sets the background text color.

+   —**blank** [*0-60**/*force**/*poke*] (virtual consoles only)
+   Sets the interval of inactivity, in minutes, after which the screen will be automatically blanked (using APM if available). Without an argument, it gets the blank status (returns which vt was blanked, or zero for an unblanked vt).
+   
+   The **force** option keeps the screen blank even if a key is pressed.
+   
+   The **poke** option unblanks the screen.

+   —**bfreq** [*nuer*] (virtual consoles only)
+   Sets the bell frequency in Hertz. Without an argument, it defaults to **0**.

+   —**blength** [*0-2000*] (virtual consoles only)
+   Sets the bell duration in milliseconds. Without an argument, it defaults to **0**.

+   —**blink** [*on**/*off*]
+   Turns blink mode on or off. Except on a virtual console, —**blink off** turns off all attributes (bold, half-brightness, blink, reverse).

+   —**bold** [*on**/*off*]
+   Turns bold (extra bright) mode on or off. Except on a virtual console, —**bold off** turns off all attributes (bold, half-brightness, blink, reverse).

+   —**clear** [*all**/*rest*]
+   Without an argument or with the argument **all**, the entire screen is cleared and the cursor is set to the ho position, just like (1) does. With the argument **rest**, the screen is cleared from the current cursor position to the end.

+   —**clrtabs** [*tab1 tab2 tab3 ...*] (virtual consoles only)
+   Clears tab stops from the given horizontal cursor positions, in the range **1**-**160**. Without argunts, it clears all tab stops.