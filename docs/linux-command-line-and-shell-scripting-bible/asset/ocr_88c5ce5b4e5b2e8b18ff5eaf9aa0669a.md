# Getting to the Shell

graphical drawings, or those who still run applications that used the vector graphics routines to draw complicated charts and diagrams.

# Display buffering

A key to graphics displays is the ability of the terminal to buffer data. Buffering data requires having additional internal memory within the terminal itself to store characters not currently displayed on the monitor.

The DEC series of terminals utilized two types of data buffering:

+   - Buffering data as it scrolled off of the main display window (called a history)
- Buffering a completely separate display window (called an alternate screen)

The first type of buffering is known as a scroll region. The scroll region is the area of memory the terminal has that enables it to "remember", as it scrolls off of the screen. A standard DEC VT102 terminal used an area for 25 lines of characters. As the terminal displays a new line of characters, the previous line is scrolled up. When the terminal reaches the bottom of the display, the next line calls the top line to scroll off the display.

The internal memory in the VT102 allowed it to save the last 64 lines that had scrolled off of the display. Users had the ability to lock the current display and use arrow keys to scroll through the previous lines that had "scrolled off" of the display. Terminal emulation packages allow you to use either a scrollbar or a mouse scroll button to scroll through the data without having to lock the display. For course, full emulation, most terminal emulation packages also allow you to lock the display and use arrow and page up/page down to scroll through the saved data.

The second type of buffering is known as an alternate screen. Normally, the terminal writes directly to the normal display area on the monitor. A method was used to quickly implement animation by using two screen areas to store data. Control codes were used to signal the terminal to write to the alternate screen instead of the current display screen. Data was held in memory. Another control could signal to switch the display between the normal screen data and the data contained in the alternate screen instantaneously. By storing successive pages in the alternate screen, then displaying them, you could crudely simulate moving graphics.

Terminals that emulate the VT100 series of terminals have the ability to support the alternative screen method.

# Color

Even back in the black-and-white (or green) dumb terminal days, programmers were experimenting with different ways to present data. Most terminals supported special control codes to produce the following types of text:

+   - Bold characters
- Underline characters