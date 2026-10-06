# VT features

The VT features commands change the features of how xterm implements the VT102/220 emulation. They include:

+   - Enable Scrollbar
- Enable Jump Scrollbar
- Enable Reverse Video
- Enable Auto Wraparound
- Enable Reverse Wraparound
- Enable Auto Linefeed
- Enable Application Cursor Keys
- Enable Application Keypad
- Scroll to Bottom on Keypress
- Scroll to Bottom on TTY Output
- Allow 80/132 Column Switching
- Select to Clipboard
- Enable Visual Bell
- Enable Pop on Bell
- Enable Margin Bell
- Enable Alternate Screen Switching
- Enable Active Icon

You can enable or disable each of these features by clicking on the feature in the menu. enabled feature will have a checkmark next to it.

# VT commands

The VT commands section sends a specific reset command to the xterm emulation window. They include:

+   - Do Soft Reset
- Do Full Reset
- Reset and Clear Saved Lines

The soft reset sends a control code to reset the screen area. This is convenient if a program sets the scroll region incorrectly. The full reset clears the screen, resets any tab positions, and resets any terminal mode feature set during the session to the initial state. The Reset and Clear Saved Lines command performs a full reset, and also clears out the scroll area history file.