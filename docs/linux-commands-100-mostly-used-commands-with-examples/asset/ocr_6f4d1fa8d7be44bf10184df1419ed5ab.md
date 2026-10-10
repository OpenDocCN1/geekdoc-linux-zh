The `stty` command in Linux is used to change and print terminal line settings. It allows users to configure various aspects of the terminal interface, such as input and output settings, control characters, and more.

# Examples:

+   1. **Display Current Terminal Settings:**

```
stty -a
```

This command displays all the current settings of the terminal.

+   2. **Change Erase Character:**

```
stty erase ^H
```

This changes the erase character to `Ctrl + H` (backspace). You can replace `^H` with the appropriate control character.

+   3. **Disable Echoing (Password Entry):**

```
stty -echo
```

This command turns off the echoing of characters as you type. Useful for password entry.