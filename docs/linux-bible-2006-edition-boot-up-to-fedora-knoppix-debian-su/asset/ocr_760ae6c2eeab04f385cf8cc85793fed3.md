After you've gathered this information, you're ready to set up your connection to the Internet. To configure Linux to connect to your ISP, read on.

# Setting Up Dial-Up PPP

PPP is used to create IP connections over serial lines. Often, the serial connection is established over a modem; however, it also works over serial cables (null modem cables) or digital lines (including ISDN and DSL).

Although one side must dial out and the other side must receive the call to the PPP connection over a modem, after the connection is established, information can flow in both directions. However, for the sake of clarity, I refer to the computer placing the call as the client and the computer receiving the call as the server.

To simplify the process of configuring PPP (and other interfaces), most Linux systems use graphical tools to configure and dial. Two tools are:

+   * Internet Configuration Wizard——Many Linux systems come with wizards that step you through setting up dial-connections. For example, from the main desktop window in Fedora and RHEL systems, choose Applications ← System Tools ← Internet Configuration Wizard. The Select Device Type window enables you to configure and test your PPP connection.

+   * KDE PPP (KPPP) Window—From the KDE desktop, select Internet ← KPPP, or from a terminal window run the kppp command. The KPPP window you set up and launch a PPP dial-connection.

Before you begin either of these procedures, physically connect your modem to your computer, plug it in, and connect it to your telephone line. If you have an internal modem, you will probably see a telephone port on the back of your computer to which need to connect. If your modem isn't detected, you can reboot your computer or run wdialconf (as described later in this chapter) to have it detected.

# Creating a Dial-Up Connection with the Internet Configuration Wizard

If you are using a Fedora or RHEL system, you can use the Internet Configuration Wizard to set up dial-networking. Here's how:

+   1. Choose Options ← System Tools ← Internet Configuration Wizard from the main menu. (Type the root password, if prompted.) A Select Device window appears (see Figure 5-7).

+   2. Select Modem connection and click Forward. The wizard searches for a modem and then the Select Modem window appears.