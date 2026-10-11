it is a control character. If you need to send the literal control character, use the function `echochar(crtype ch)`.

> **NOTE**
> The ncurses documentation refers to characters typed in `ctype` format as "pseudocharacters." ncurses declares pseudo-characters as unsigned long integers, using the high bits of these characters to carry additional information, such as video attributes. This distinction between pseudo-characters and normal C characters (the char type) implies subtle differences in the behavior of functions that handle each type. These differences are noted in this chapter when and where appropriate.

As mentioned previously, `mvadddch` adds a character to a specified window after moving the cursor to the desired location; `mvwaddch` combines a move and an output operation on a specific window, `wadddch` displays a character to a user-specified window. The `echochar` function, and its window-specific cousin, `wechochar`, combine an `adddch` call with a `refresh` or `wrefresh` call. This combination can result in substantial performance enhancements when used with non-control characters.

A particularly useful feature of ncurses routines that use `ctype` characters and strings (discussed next) is that the character or string to be output can be logically ORed with a variety of video attributes before it is displayed. A partial list of these attributes includes:

+   * `A_NORMAL`—Normal display mode
+   * `A_STANDOUT`—Use the terminal's best highlighting mode
+   * `A_UNDERLINE`—Underlining
+   * `A_REVERSE`—Use reverse video
+   * `A_BLINK`—Blinking text
+   * `A_DIM`—Half-intensity display
+   * `A_BOLD`—Extra-intensity display
+   * `A_INVIS`—Character will not be visible
+   * `A_CHARTEXT`—Creates a bitmask to extract a character

Depending on the terminal emulator or hardware capabilities of the screen, not all attributes may be possible or will necessarily display correctly, however. See the `curs_attr(3)` manual page for more details.

In addition to control characters and characters enhanced with video attributes, the character output functions also display line graphics characters (characters from the high half of the ASCII character set, 128–255), such as box-drawing characters and various special symbols. A complete list is