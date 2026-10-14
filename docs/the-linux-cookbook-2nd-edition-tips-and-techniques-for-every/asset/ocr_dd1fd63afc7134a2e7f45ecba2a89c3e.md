⇒ To run the vi tutorial, type the following from your home directory:

```
$ cp /usr/doc/nvi/vi.beginner.gz . RET
$ gunzip vi.beginner.gz RET
$ vi vi.beginner RET
```

**NOTES:** An advanced tutorial is also available in /usr/doc/nvi.

The vim editor has an interactive tutorial that you run as its own command, vimtutor.

# 10.2.3 Using Basic Vi Editing Keys

Editing keys depend on the mode you are in. When in insert mode, any text you type is inserted in the file until you type ESC to switch back to command mode.

The following table describes commands available when in command mode.

*Cursor Movement*

| Key | Description |
|---|---|
| CTRL-(F) | Scroll text down one full screen. |
| CTRL-(B) | Scroll text up one full screen. |
| CTRL-(D) | Scroll text down one half-screen. |
| CTRL-(U) | Scroll text up one half-screen. |
| ↓ or j | Move down one character. |
| ↑ or k | Move up one character. |
| ← or h | Move to the left one character. |
| → or l | Move to the right one character. |
| H | Move to top of screen. |
| L | Move to bottom of screen. |
| w | Move forward one word. |
| b | Move backward one word. |
| ( | Move forward one sentence. |