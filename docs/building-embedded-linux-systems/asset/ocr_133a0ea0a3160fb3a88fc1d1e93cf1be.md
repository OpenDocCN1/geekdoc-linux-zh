![](bbox=[0.14, 0.1, 0.86, 0.6])

> *Figure 4-14. Eclipse Remote System Type wizard*

Run and Debug menus, allowing you to run and debug your application remotely on the target board.

For further discussion of debugging with Eclipse, see “Eclipse” in Chapter 11.

# Terminal Emulators

The most common way to communicate with an embedded system is to use a terminal emulation program on the host and communicate through an RS232 serial port with the target. Although there are a few terminal emulation programs available for Linux, not every one is fit for all uses. In the past, there have been well-known problems between minicom and U-Boot, for instance, during file transfers over the serial port. Hence, we recommend that you try more than one terminal application to communicate with your target. If nothing else, you are likely to discover one that best fits your personal