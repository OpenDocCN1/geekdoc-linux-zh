```
#else
    /* some fallback code here */
#endif
}
```

We will omit the fallback code for now, since it requires knowing more about terminals.

The second problem is how to remove the old more? prompt so that it does not scroll up the screen. In short we need a way to clear portions of the screen. We also need a way to move the cursor to various places on the screen. There are various ANSI escape sequences that do these things. The table below lists a small fraction of the set of ANSI escape sequences. The ones in the table are the easiest to learn and use. In the table, the symbol "ESC" is short for '\033'. In almost all cases, the default value of n in the table is 1.

| Key Sequence | Meaning |
|---|---|
| ESC[M | Move the cursor up in scrolling region. |
| ESC[nA | Move the cursor up n lines. |
| ESC[nB | Move the cursor down n lines |
| ESC[nC | Move the cursor right n columns |
| ESC[nD | Move the cursor left n columns |
| ESC[nG | Move the cursor to column n |
| ESCE | Move cursor to start of next line |
| ESC[r;cH | Move the cursor to row r, column c. |
| ESC[0K | Erase from the cursor to the end of the line |
| ESC[1K | Erase from the beginning of the line to the cursor. |
| ESC[2K | Erase the line |
| ESC[0J | Erase from the cursor to the end of the screen. |
| ESC[1J | Erase from the bottom of the screen to the cursor |
| ESC[2J | Erase the screen |
| ESC[0m | Normal characters |
| ESC[1m | Bold characters |
| ESC[4m | Underline characters. |
| ESC[5m | Blinking characters |
| ESC[7m | Reverse video characters |
| ESC[g | Clear tab stop at current column. |
| ESC[3g | Clear all tab stops. |

# Examples

Following are a few examples of sequences of commands. The last two are compound control sequences, and they are of significance because we can use them in our program.