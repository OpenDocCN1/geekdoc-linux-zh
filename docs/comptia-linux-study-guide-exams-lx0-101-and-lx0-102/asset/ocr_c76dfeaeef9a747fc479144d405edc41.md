# Configuring Basic X Features 281

**FIGURE 6.1** Modern desktop environments provide easy-to-use but limited X configuration options.

![](bbox=[0.312, 0.146, 0.687, 0.391])

# Obtaining X Display Information

Sometimes it's helpful to know about the capabilities of your display, as it's managed by X. The tool for this job is **xdpyinfo**. When you type **xdpyinfo**, the result is copious information about the current display, such as the X version number, the resolution and color depth of all the current displays, and so on. Much of this information is highly technical in nature, so you may not understand it all. That's OK recommend you run this program and peruse the output to see what you can learn from it. If you later want to obtain similar information on another computer's display, you'll know how to obtain it.

For more technical information, you can use the **-ext extension** option to **xdpyinfo**. The **extension** is the name of an X extension, a software module that provides extended capabilities to X. (The basic **xdpyinfo** command, without options, lists all the available extensions.)

You can obtain detailed technical information about a specific window with the **xinfo** command. In basic use, you type **twininfo**, move the cursor over a window, and click. The result is a list of assorted data about the window you clicked, such as the following:

+   - Absolute upper-left X: 1171
- Absolute upper-left Y: 611
- Relative upper-left X: 6
- Relative upper-left Y: 25
- Width: 657
- Depth: 32