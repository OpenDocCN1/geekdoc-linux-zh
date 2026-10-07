# Detecting and Configuring a Modem

You can also use Red Hat's graphical X client to configure a modem after the initial Red Linux installation. Internet connection software such as Red Hat's -config-network client (shown in Figure 4.7) will try to probe the system for an available modem. If a modem is not found, you can manually enter modem data.

![](bbox=[0.143, 0.196, 0.853, 0.473])

FIGURE 4.7 The Red Hat Linux redhat-config-network client will probe for an available modem.

KDE provides the kppp client (shown in Figure 4.8) that can also be used to look for and set up a modem when you set up a new Point-to-Point Protocol (PPP) connection. Click the Query Modem button in kppp's dialog to search for an installed modem.

Red Hat Linux includes command-line-based diagnostic and serial-port configuration tools for the system administrator. For example, to get more information about a specific port, you can use the staterial command, along with a designated device like this:

```
# staterial /dev/ttyS0
Device: /dev/ttyS0
```

Signal Pin Direction Status Full
Name (25) (9) (computer) Name

| FG | 1 | - Frame Ground |
| TxD | 2 3 out | - Transmit Data |
| RXD | 3 2 in | - Receive Data |
| RTS | 4 7 out | 1 Request To Send |
| CTS | 5 8 in | 0 Clear To Send |