To simplify the process of configuring PPP (and other network interfaces), Red Hat Linux lets you configure dial-up by using either the Internet Configuration Wizard or another tool, such as kppp:

+   - **Internet Configuration Wizard** — From the main desktop menu, choose System Tools → Internet Configuration Wizard. The Select Device Type window that appears lets you configure and test your dial-up PPP connection.

+   - **KPPP Window** — From the KDE desktop, select Internet → More Internet Applications → KPPP, or from a Terminal window run the kppp command. From the KPPP window you can set up a PPP dial-up connection and launch it.

Before you begin either of the two dial-up procedures, physically connect your modem to your computer, plug it in, and connect it to your telephone line. If you have an internal modem, you will probably see a telephone port on the back of your computer that you need to connect. If your modem isn't detected, you can reboot your computer or run wvdialconf create (as described later in this chapter) to have it detected.

# ## Creating a dial-up connection with the Internet Configuration Wizard

Use the Internet Configuration Wizard to set up dial-up networking. To start it, choose System Tools → Internet Configuration Wizard from the main menu. (Type the root password, if prompted.) A Select Device Type window appears to help you select the device for your Internet connection (a dial-up modem, in this case), as shown in Figure 16-1.

![](bbox=[0.078, 0.556, 0.56, 0.83])

Figure 16-1: The Internet Configuration Wizard helps you set up a PPP Internet connection.

Follow the procedure below from the first Select Device Type window.