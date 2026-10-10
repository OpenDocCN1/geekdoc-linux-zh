+   - normal. Uses normal VGA text mode.
+   - extended. Attempts to use 80×50 text mode.
+   - ask. Just before booting, prompts for a number, corresponding to a displayed text mode.

Results between different notebooks will vary. For example, at the LILO boot: prompt, you can try this:

boot: vga=ask

Press Enter. You might see an error message like this:

```
No such image. [Tab] shows a list.
```

Press Backspace, and then press Enter again. You'll see this:

```
Loading Linux……
Press <RETURN> to see video modes available. <SPACE> to continue or wait 30 secs
```

Press Enter to display the video modes. You'll then see this (depending on your notebook):

```
Video adapter: VESA VGA
Mode:    COLUMNS×ROWS:
0  0F00  80×25
1  0F01  80×50
2  0F02  80×43
3  0F03  80×28
4  0F05  80×30
5  0F06  80×34
6  0F07  80×60

Enter mode number or 'scan':
```

You can then enter a number, such as 2, and press Enter. Linux will boot and attempt to use the console font you selected. If you enter the keyword scan and press Enter, the screen will blank for 5 or more seconds, and you'll again see a list of text modes. These modes represent the capabilities of your notebook, and are a better list of modes to try.

# ## Remapping the X11 Keyboard

Manually remapping your X11 keyboard using various X11 clients and the xmodmap client could be a tedious task. However, thanks to Jamie Zawinski's xkeycaps client, you can scroll through a list of hundreds of keyboards and quickly reconfigure