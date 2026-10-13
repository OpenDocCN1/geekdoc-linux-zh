A third way to diagnose, check, or reset your PC cards, if you're using X11, is with David Hind's cardinfo client. Start cardinfo from the command line of a terminal window like this:

```
# cardinfo
```

After you press Enter, you see a window somewhat like that in Figure 3.5.

# FIGURE 3.5

The cardinfo X11 client can be used to monitor, reset, suspend, eject, or insert PC cards with OpenLinux.

![](bbox=[0.26, 0.35, 0.56, 0.62])

A small log window in the lower left of the cardinfo dialog box lists PC card events, such as insertion or removal. To control a card, press and hold down a card's Socket button. You'll see a small menu enabling you to reset, eject, or insert a card.

# Configuring Network Information with COAS

Although you were asked for network information during your OpenLinux installation, this is not your only opportunity to configure an interface. If you didn't enter network information during the installation, you don't have to perform a re-install just to configure networking! Use the COAS utility to configure your interface's address.

# Configuring Your Ethernet Interface

To configure your interface, click the Application Starter button in your KDE desktop, select COAS and then Network, and click on Ethernet Interfaces, as shown in Figure 3.6.