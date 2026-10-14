# TABLE 27.2 CONTINUED

| GXandReverse | source AND NOT destination |
| GXcopy | source |
| GXandInverted | NOT source AND destination |
| GXnoop | destination |
| GXxor | source XOR destination |
| GXor | source OR destination |
| GXnor | NOT source AND NOT destination |
| GXequiv | NOT source XOR destination |
| GXinvert | NOT destination |
| GXorReverse | source OR NOT destination |
| GXcopyInverted | NOT source |
| GXorInverted | NOT source OR destination |
| GXnand | NOT source OR NOT destination |
| GXset | 1 |

# KEYBOARD INPUT EVENTS

Of the two keyboard input events, KeyPress and KeyRelease, only the first is guaranteed to be available. The X server reports KeyRelease events only on hardware that provides the necessary signal from the keyboard. So, never count on obtaining KeyRelease events (most, if not all, Linux PC installations should support this event, however).

Because of great differences among keyboards on UNIX and Linux hardware, you cannot simply look up a key code as reported in a KeyPress or KeyRelease event. Instead, you must go through an intermediate step to map a key’s event code with a value in the server’s data tables for a value that represents a specific key. The result is a symbol such as XK_UP and XK_Home. Listing 27.6, xkey.cpp, demonstrates how to detect KeyPress events, look up the symbolic value in the server’s key mapping, and display the key’s name if it has one. As in most of this chapter’s listings, to save space, only the relevant statements are printed here. Compile and run the program, and press any key to see its string name and translated, symbolic value in decimal. Press Esc to quit. Figure 27.4 shows a sample output window.

Figure 27.4
Sample xkey window.

![](bbox=[0.27, 0.89, 0.48, 0.97])