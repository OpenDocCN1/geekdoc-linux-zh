| Command | Moves the Cursor . . . |
| :--- | :--- |
| b | To the previous word |
| 0 (zero) | To the start of the line |
| $ | To the end of the line |
| Ctrl+F | One page up |
| Ctrl+B | One page down |
| G | To the end of the file |
| 1G | To the top of the file |
| xG | To line number x |

Are you enjoying working with vi? It can do a lot more. Try combining commands. For example, in command mode, typing

```
`d$`
```

deletes all the text from the cursor to the end of the line.

Well, should you know more? Being able to save a file would be convenient:

+   1. **Type `:` (colon) to switch to last-line mode.**
+   2. **Type one of the following:**
+      * `w` to save the file
+      * `wq` (write and quit) to save the file and exit vi

If you want to exit without saving, typing `q!` is all you have to do.

![](bbox=[0.07, 0.66, 0.13, 0.75])

To find out more about using vi, type `man vi` to check out its manual pages.