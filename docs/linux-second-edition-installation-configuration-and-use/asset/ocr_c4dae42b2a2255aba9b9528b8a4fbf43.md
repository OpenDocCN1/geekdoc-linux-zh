Combinations with Ctrl-z, where z can be any letter (but not a digit or special character). Similarly, the letter S is used for Shift, M for Meta Esc and A for Alt. For function keys, the backslash (\ for letters C, S, M and A can be omitted (thus, [S-f1]). Some further examples will clarify the syntax:

# GNU Emacs keyboard shortcuts

| [?a] | Ctrl+X x Y Z |
| [f1] | [?C-x y ?][M-z] | Ctrl+X Shift+Alt+Z |
| [?C-x] | Ctrl+X [?C-x f1] | Ctrl+X F1 |
| [?W-w] | Alt+W [S-right] | Shift+|
| [?e] | Esc |

# Xeacs syntax for keyboard shortcuts

In Xeacs, keyboard shortcuts must in addition enclosed in parentheses. Keys corresponding letters are simply coded by the letter itself, with upper and lower case being significant. Status keys are expressed by the keywords shift, control and meta (for Alt). Because of the parentheses, no hyphens are required between the keywords. Generally, these rules lead to more readable code. Some examples:

# Xeacs keyboard shortcuts

| [a] | A |
| [A] | Shift+A |
| [(meta a)] | Alt+A |
| [(control x) (meta a)] | Ctrl+X Alt+A |
| [(shift end)] | Shift+End |

# Key codes of important special keys

In order to save you too much when experimenting with key combinations, the following list shows the most important special keys under X. The list equally applies to GNU Emacs and Xeacs. Please note that depending on your Linux distribution and the xmodmap setting and versions used, the results may be different.

# Key codes of special keys

| [↑] | PgUp [prior] |
| [↓] | PgDn [next] |
| [←] | Home |
| [→] | End |