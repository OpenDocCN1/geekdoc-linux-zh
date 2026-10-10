# **Appendix D**

# ## ASCII Character Codes

Use the charts displayed in Figures C.1 and C.2 to view all 256 ASCII character codes. To access the characters that aren't available on the keyboard, simply use a construction like the following:

```
```text
int num;

char c[] = {num, '\0'};
```
```

Here, num is the ASCII value in question. For example, if the value of num were 156, character c would be the symbol for pounds sterling (£).

An alternate method exists for PC users who have extended (101 or 104-key) keyboards. Simply press and hold down either Alt key and use the numeric keypad on the right side to input the ASCII value in question. For instance, typing Alt+1+5+6 (without the plusses) would yield the same symbol (£) as before. Just don't let up on the Alt key between numbers. This feature isn't specific to Linux, but rather to the extended keyboard, so you're able to use this trick on any other operating system that utilizes PC hardware.

467