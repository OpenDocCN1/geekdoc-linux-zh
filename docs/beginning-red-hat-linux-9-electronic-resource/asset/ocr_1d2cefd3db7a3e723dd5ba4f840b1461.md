In this section we'll take a look at how to set up a Linux machine as a DHCP server.

# Installing the DHCP Server Packages

As you've probably already gathered, you only need one DHCP server per network. If you decide that you need a DHCP server, then a Red Hat Linux 9 machine will suit your purposes. To configure your machine as a DHCP server, you need to install the appropriate package, and (you've guessed it) we can do that via the RPM GUI.

To do this, launch the RPM GUI (via Main Menu | System Settings | Add/Remove Applications, for example); when the dialog appears, select the Network Servers package group (which you'll find under the Servers category). Click on the Details button to view the package details:

![](bbox=[0.17, 0.28, 0.86, 0.75])

The package we need here is the one called dhcp - the others are not important for the purposes of installing a DHCP server (though you won't want to deselect them unless you're sure you're not using them for something else!).

When you've selected dhcp, click on Close and then on Update to start the installation. As usual, you'll need the distribution CDs in order to complete the installation.