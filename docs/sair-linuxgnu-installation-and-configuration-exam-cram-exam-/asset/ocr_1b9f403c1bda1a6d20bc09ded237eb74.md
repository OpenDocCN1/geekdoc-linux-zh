# Mouse

As shown in Figure 10.3, you can customize your mouse in any number of ways. But the key objective is to get a working mouse. All other items shown in Figure 10.3 that are not described in the following list are less important. To get a working mouse, choose from the following options:

+   - **Protocol**—The protocol you choose selects a driver, which determines how your computer communicates with your mouse.
+   - **Device**—The mouse device is based on how your mouse is connected to your computer. Although a PS/2 mouse is set up for the /dev/psaux device, a serial mouse is generally attached to a COM port. If you don't see an option for COM ports, you should see something like /dev/ttyS0 or /dev/cua0, which corresponds to COM1 (/dev/ttyS1 or /dev/cua1 corresponds to COM2, etc.).
+   - **3 Buttons**—If you only have a two-button mouse, you'll want to emulate three buttons. The middle button is used for a number of Linux GUI pop-up menus including copy and paste operations.

*Note: You can't configure special devices, such as joysticks and graphic tablets, with XFree86Setup. If you want to use one of these devices in a Linux GUI, you'll need to add its settings directly to the /etc/X11/XF86Config.file.*

![](bbox=[0.12, 0.6, 0.88, 0.9])

Figure 10.3 XF86Setup mouse configuration options.