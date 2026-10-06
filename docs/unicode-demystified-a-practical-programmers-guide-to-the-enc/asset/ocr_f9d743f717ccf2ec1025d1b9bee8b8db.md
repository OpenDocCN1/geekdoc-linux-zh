# Tutorial: Creating and Editing a File with vim 47

![](bbox=[0.355, 0.075, 0.785, 0.315])

**Figure 10-3** Modes in vim

command vim to enter Input mode. In Input mode accepts anything you enter as text and displays it on the screen. Press ESCAPE to return vim to Command mode.

By default the vim editor you informed about which mode it is in: You will see --INSERT-- at the lower-left corner of the window while you are in Insert mode. The following command causes vim not to display the mode it is in while you are entering text:

+   - set noshowmode

The colon (:) in this command puts vim into another mode, Last line mode. While this mode, vim keeps the cursor on the bottom line of the screen. When you finish the command by pressing RETURN, vim restores the cursor to its place in the text. Input modes are Open, Insert, and Append. Refer to “Show mode” on page 453. Refer to page 422 for an explanation of Change and Replace.

When you give vim command, remember that the editor is case sensitive. The vim editor interprets the same letter as two different commands, depending on whether you enter an upper- or lowercase character. Beware of the key that causes your keyboard to set only uppercase characters; CAPS LOCK or SHIFT. If you set this key to uppercase while you are in Input mode and exit to Command mode, vim interprets your commands as uppercase letters. It can be very confusing when this happens because vim does not appear to follow the commands you are giving it.

# Entering Text

When you start a new session with vim, you must put it in Input mode before you can enter text. To put vim in Input mode, press the i key (insert before the cursor) or the a key (append after the cursor).