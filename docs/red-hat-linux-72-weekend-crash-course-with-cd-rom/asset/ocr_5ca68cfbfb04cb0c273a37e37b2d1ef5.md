| J | Joins the current line with the next one. |

| rx | Replaces the character under the cursor with *x* (*x* is any character). |

| Move cursor |
| h | Moves one character to the left. |
| j | Moves one line down. |
| k | Moves one line up. |
| L | Moves cursor to the end of the screen. |
| l | Moves one character to the right. |
| w | Moves to the beginning of the following word. |

| Scroll text |
| Ctrl-b | Scrolls backward by one full screen. |
| Ctrl-d | Scrolls forward by half a screen. |
| Ctrl-f | Scrolls forward by one full screen. |
| Ctrl-u | Scrolls backward by half a screen. |

| Cut and paste text |
| P | Puts a yanked (copied) line above the current line. |
| p | Puts a yanked line below the current line. |
| yy | Yanks the current line into an unnamed buffer. |

| Colon commands |
| :command | Executes the shell *command*. |
| :q | Quits the editor. |
| :q! | Quits the editor without saving changes. |
| :r *filename* | Reads a file and inserts text after the current line. |
| :w *filename* | Writes a buffer to a file. |
| :wq | Saves changes and exits the editor. |

| Search text |
| /string | Searches forward for *string*, a series of one or more characters. |
| ?string | Searches backward for *string*, a series of one or more characters. |

| Miscellaneous |
| u | Undoes the last command. |
| Esc | Ends input mode and enters visual command mode. |
| U | Undoes recent changes to the current line. |