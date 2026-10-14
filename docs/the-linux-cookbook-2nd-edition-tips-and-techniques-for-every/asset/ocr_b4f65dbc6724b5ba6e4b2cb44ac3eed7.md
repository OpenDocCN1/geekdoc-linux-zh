# METHOD #2

To display raw control characters in text, but try to keep the screen appearance, use less with the -R option. This displays raw control characters, but any disparities that may be caused by the control characters on the screen are controlled, whenever possible.

+   ⇒ To peruse the file `live.transcript` and display any raw control characters in it, but attempt to keep the screen in order, type:

```
`$ less -R live.transcript` (RET)
```

# 9.1.5 Perusing Multiple Text Files

There are two methods for perusing multiple text files.

![](bbox=[0.106, 0.423, 0.849, 0.769])

*Figure 9-1. Viewing multiple files in less.*

# METHOD #1

You can specify more than one file page through with less, and you can specify file patterns in order to open all of the files that match that pattern. The files will be displayed in sequence—less displays each file in turn, beginning with the first file you specify or the first file that matches the given