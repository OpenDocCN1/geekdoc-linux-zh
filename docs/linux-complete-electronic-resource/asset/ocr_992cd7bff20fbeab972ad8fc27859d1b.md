Once you have your stty settings right, so that cat `file > /dev/ttyS2` (in my case) sends the file to the printer, look at the file `/usr/src/linux/include/asm-1386/termbits. h`. This contains a lot of defines and a few structs (You may wish to cat this file to the printer [you do have that working, right?] and use it as scratch paper). Go to the section that starts out

```
/* c_cflag bit meaning */
#define CBAUD 0000017
```

This section lists the meaning of the fc and fs bits. You will notice that the names there (after the baud rates) match up with one of the lines of stty output. Didn’t say this was going to be easy?

Note which of those settings are preceded with a - in your stty output. Sum up all those numbers (they are octal). This represents the bits you want to clear, so the result is your fc capability. Of course, remember that you will be setting bits directly after you clear, so you can just use fc0177777 (I do).

Now do the same for those settings (listed in this section) which do not have a - before them in your stty output. In my example the important ones are CS8 (0000060), HUPCL (0002000), and CREAD (0000200). Also note the flags for your baud rate (mine is 0000015). Add those all up, and in my example you get 0002275. This goes in your fs capability (fs02275 works fine in my example).

Do the same with set and clear for the next section of the include file, c1flag bits. In my case I didn’t have to set anything, so I just use xc0157777 and xs0.

# # Older Serial Printers that Drop Characters

Jon Luceky points out that some older serial printers with ten-cent serial interfaces and small buffers really mean stop when they say so with flow control. He found that disabling the FIFO in his Linux box’s 16550 serial port with setserial corrected the problem of dropped characters (you apparently just specify the uart type as an 8250 to do this).