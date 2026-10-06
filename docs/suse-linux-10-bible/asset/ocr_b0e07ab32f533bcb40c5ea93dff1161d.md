# Chapter 11 ✦ Text Editors 307

```
This is line 1
This is line 2
This is line 3
This is line 4
This is line 5
This is line 6
This is line 7
This is line 8
This is line 9
This is line 10
```

![](bbox=[0.182, 0.129, 0.816, 0.503])

# Copying and Pasting

Entering copious amounts of text into a file is never a fun thing, and the copy-and-npaste idea has helped to speed up repetitive text entry. In most graphical user-interface (GUI) applications, a simple right-click for the text menu enables you to copy\and paste text. When you are working on the command line, this is not possible,
and you have to do it a little differently.

In `vim`, you call a `yank` (as in, you are yanking the text). With this mind,
y may be able to guess what you use to yank the text, `y+y` combination. To
copy a line of text, place your cursor on the line you want to copy and press `y+y`.
This copies the text into the buffer. To paste the line to another place in the file,
press `p` key (for paste).

If you wanted to paste multiple copies of the line, you can use the multiplier. For
example, to paste a line five times, use `5+p`.