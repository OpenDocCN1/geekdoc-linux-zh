# # vi / vim

**Purpose**: Full featured text editor.

**Usage syntax**: `vi/vim [OPTIONS] [FILE]`

```
$ vim ShoppingList.txt
Milk
Eggs
Cheese
Tacos
~
~
~
~
~
~
~
~/home/nick/ShoppingList.txt" 4 lines, 19 characters
Using vi to edit a text file
```

The `vi` editor (also known as `vim`) is a complex and full featured text editor for Unix, Linux, and BSD systems. Traditional Unix systems typically utilize `vi` as the default text editor. Modern Linux and BSD systems use `vim` which is an enhanced version of `vi`.

The `vi` and `vim` editors have two basic modes of operation: command mode and editing mode. Pressing `Esc` on the keyboard activates command mode. When in command mode, command keys can be used to activate specific editing functions. The following table lists the most common commands for `vi` and `vim`.

| Key(s) | Function | Key(s) | Function |
| :--- | :--- | :--- | :--- |
| `:w` | Save | `A` | Append text after |
| `:x` | Save and exit | `r` | Replace text before cursor |
| `:q` | Quit | `R` | Replace text after cursor |
| `i` | Insert text before | `YY` | Copy current line |
| `I` | Insert text after | `p` | Paste copied text |
| `a` | Append text before | `/ [TEXT]` | Search for the specified text |

Command keys for vi and vim

+   Common usage examples:
+   `vi [FILE]` Open the specified file for editing in vi
+   `vim [FILE]` Open the specified file for editing in vim
+   `view [FILE]` Open the specified file in read only mode