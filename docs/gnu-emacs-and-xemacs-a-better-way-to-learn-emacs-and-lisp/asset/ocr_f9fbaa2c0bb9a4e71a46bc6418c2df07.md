A keymap can be global, effective in all Emacs buffers and modes, or local, confined to buffers of a certain type. Each time you use a keyboard command, Emacs first looks for that key sequence in the local keymap (which may be part of a mode). If the key sequence isn't found, the global keymap is consulted; if a match is found, the associated command is executed. If Emacs draws a complete blank, the error message (keys pressed) not defined appears in the minibuffer. This sounds like a slow process, but because the keymaps are maintained in memory, access to them is near-instantaneous.

The global keymap isn't merely a jumbled heap of keybindings. It's sorted according to prefix; each prefix (such as Ctrl-x) has its own subkeymap. All key commands that begin with Ctrl-x (such as Ctrl-x h, the kill buffer command) are part of the ctrl-x-map. Adding a new keybinding to the global keymap requires a Lisp expression like this one:

```
```lisp
(global-set-key [(control c) c] 'fill-region)
```
```

The function global-set-key is a built-in Emacs function; its first argument is the key representation, and the second is the command to run. In this example, I've defined the keybinding for the built-in function fill-region (which re-fills all the paragraphs in the selected region) to be Ctrl-c c. This function has no default keybinding. If there had been one, it would still be in effect and you would end up with two keybindings for the same command.

The single quote just before fill-region is necessary, because it forces the global-set-key function to treat fill-region as a symbol rather than as a variable's value.

Many Emacs commands use the Ctrl key pressed simultaneously with a letter key (known as the modifier), followed by either a single letter key or another Ctrl key-modifier combination. One of these combinations has been reserved for your new keybindings: the Ctrl- prefix. This prefix is easy to type and should be your first choice when you need a keybinding for a newly-created command.

Another possibility is to change a default Emacs keybinding. This is called re-binding a keyboard command. There are most likely several keybindings that you never use and can't foresee using in the future. As an example, consider the Ctrl-z keybinding. Pressing it suspends Emacs and iconifies the frame. Any Linux window manager provides the same action, either with a title-bar button or as a menu item, so this might be a candidate for re-binding.

Perhaps you find the default keybinding for beginning-of-buffer (M-<) awkward to press. The following line in your ~/.emacs file assigns Ctrl-z to this command:

```
```lisp
(global-set-key [(control z)] 'beginning-of-buffer)
```
```