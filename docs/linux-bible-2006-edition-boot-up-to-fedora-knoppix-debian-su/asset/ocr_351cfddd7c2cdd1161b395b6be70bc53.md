# 194 Part II ♦ Running the Show

If the modem wasn't detected, you should determine whether it is a modem supported in Linux. You can do this by finding out what type of chip set is used in the modem. This is even more important than finding out the manufacturer of the modem because the same manufacturer can use chips from different companies. (This applies primarily to internal modems because most external serial modems and USB modems are supported in Linux.)

After you have detected the chip set being used, the Linmodems.org's Website (www.linmodems.org), which contains information on so-called Winmodems that have only recently begun to be supported in Linux. Search for the chip set on your modem from this site. In many cases, the site can tell you if there is a driver for your modem.

# Summary

There are many different tools for configuring network connections in the various Linux distributions. Fedora and other Red Hat Linux systems use a graphical Network Configuration. SUSE Linux uses its YaST administrative interface to configure network equipment. For dial-up networks, the KDE desktop includes the kpppp GUI tool for configuring modems. If your network connection doesn't start up automatically (as it does in many cases), this chapter explains how to use some of these network configuration tools to configure it manually.

By adding your computer to a public network, such as the Internet, you open it to possible intruders. The next chapter describes ways in which you can secure your computer from unwanted access.