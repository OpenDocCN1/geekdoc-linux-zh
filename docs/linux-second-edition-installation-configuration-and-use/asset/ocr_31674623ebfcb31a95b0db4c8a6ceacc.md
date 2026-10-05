# Colors and special keys in xterm/nxterm

RedHat developers have an inexplicable predilection for black (n)xterm windows with tiny writing. If you want to enjoy your eyesight a bit longer, a first-aid recommendation is to delete or rename .xdefaults. Even better results are achieved with the following .xdefaults file, which at the same time looks after proper functioning of the keys.

```
! .xdefaults #override \
VT100.Translations: #override \
<KeyPress>Backspace: string(0x7f)\n
<KeyPress>delete: string(0x04)\n
VT100:font: 9x15
VT100:background: white
VT100:foreground: Black
xterm*scrollBar: true
```

Unfortunately, this setting has no validity for gnome-terminal. Here you can easily change the color scheme via a menu, a configuration possibility for [Ctrl|D] seems to be liking.

# Confirmation prompts with mv and rm

When you work as root, during execution of mv and rm continuous prompts appear for confirmation of whether you really want to carry out the operation. These confirmation prompts stop when you remove the aliases from ~/.bashrc.

# Display system messages at start-up

During start-up of Linux kernel and various Init-V scripts display messages on screen. However, these messages are deleted as soon as the login prompt appears. Since these messages may under certain circumstance allow conclusions to be drawn on possible configuration problems, this behavior is not very smart. This can be remedied with a small modification in /etc/inittab: add the option --nuclear at the start of getty for console 1.

```
# /etc/inittab
1:12345:respawn:/sbin/mingetty --nuclear tty1
```

# Control Panel

The control-panel program can be started by root. It allows an easy start of the RedHat configuration tools, which are described in the following subsections.

The individual tools can obviously be started directly, without using control-panel. Despite the user-friendly interface, handling of these programs assumes a solid background knowledge. If in doubt, read the sections on manual configuration of the affected files (Chapter 6).