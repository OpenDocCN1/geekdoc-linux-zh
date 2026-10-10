in the Xconfig file.

**FontPath** *<string>* FontPath is followed by a comma-delimited string of font directories. A font directory is any directory which contains fonts and a fonts.dir file.

**HotKeyExit** This allows you to shut down the X server with the key sequence Ctrl - Alt - Backspace . If this keyword is not present, Ctrl - Alt - Backspace does nothing special.

**KbdDesc** *<string>* The quoted string must match one of the entries in the KeyboardInfo file.

**KbdDescFile** *<string>* The string describes the keyboard.

**LogFile** *<filename>* Errors from the X server are logged here.

**Modes** The entries following the Modes give display mode timing information. If more than one mode is specified, the server can switch between modes. See Modes (section B.2.4 for more details.

**Monitor** *"<string>"* The quoted string must match one of the entries in the MonitorInfo file. Mouse<type> <device> This describes the type of mouse in use. Type is a keyword that is OS dependent; the device parameter is usually required and is a file in the /dev directory.

**MouseDesc** *"<string>"* The quoted string must match one of the entries in the MouseInfo file.

**ScreenLayout** *<screen>*<left_neighbor>*<right_neighbor>*<top_neighbor>*<bottom_neighbor>*<left_edge>*<right_edge>*<top_edge>*<bottom_edge>* This defines how the mouse cursor behaves when it gets to the edge of the screen. There is one ScreenLayout entry for each configured screen. The * _neighbor fields tell which screen to move the mouse to. A value of -1 indicates that the mouse should stop at that edge. The * _edge fields tell at which edge of the corresponding * _neighbor screen the mouse will appear. Screens are numbered from 0 to 4. Edges are numbered as follows:

> **NOTE:** Any changes made to this entry will be lost if configX is run.

**ScreenLayoutIndex** *<number>* This tells which of the predefined screen layouts was chosen in configX.