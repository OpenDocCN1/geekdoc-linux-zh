Taciturn Mr. Debug, this means, “Begin accepting entered bytes at address 010EH. I show the lowercase Es used in the command to put across the point that DEBUG is not sensitive to case, even for letters used as hexadecimal digits. In other words, there is nothing sacred about using uppercase A through E for hex digits. They can be lowercase or upper-case as you choose, and you don't even have to be consistent about it.

What DEBUG does in response to the E command shown in Figure 4.6 is display the following prompt:

```
38E3:010E 61.
```

The cursor waits after the period for your input. What DEBUG has done is shown you what value is at address 010EH, so that you can decide whether you want to change it. If not, just press Enter, and the dash prompt will return. Here, it's asking you you want to replace the value 61. There's no H after it, but you must never forget that DEBUG always works in hex. That “61” is intended to be 61H.

Otherwise, a hexadecimal value to take the place of value 61H. In Figure 4.6, I wanted to use 6FH, and typed “6f.” Don’t type the H! Once you use a replacement value, but before you Enter, you have two choices:

+   That is all, in fact, that you wish to change. Press Enter and return to the dash prompt.

+   You wish to change the byte at the next address as well. In this case, press the space bar instead. DEBUG will display the byte at the next highest address and wait for your replacement value, just as it did the first time.

This is shown in Figure 4.6. Figure 4.6 shows successive replacements of bytes starting at address 010EH. Notice the lonely hex byte 0A followed by a period. What happened there that I pressed Enter without typing a replacement byte, ending the E command and returning to the dash prompt.

You’ll also note that the next command typed at the dash prompt was “q.” for Quit. Tipping Q at the dash prompt will return you immediately to DOS.

# The Dangers of Modifying Files

Keep in mind that what I’ve just demonstrated was not changing a file, but simply changing the contents of a file loaded into memory. A file