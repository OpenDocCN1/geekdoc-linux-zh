Internet Connection Sharing. If you are on a small or home network that does not have a computer acting as a dedicated server for the Internet connection to the rest of the computers on the network, some computer has to step up and volunteer for the job. If yours is the computer on your network that is directly connected to the Internet, this module walks you through a wizard of choices so that you can share that connection with other computers on your network.

# TOOL KIT: 3.5

# Setting Up Your LAN Connection in Mandrake

Mandrake puts everything in one place for you, making it easier to find, but the interfaces for some of the tools are a bit clumsy. Nonetheless, it is a wizard, so let’s step through it.

+   1. From the MandrakeLinux Control Center, click Network & Internet > New Connection.
+   2. The first step is to choose a connection type. Click LAN Connection and then click Next.
+   3. Choose your network card from the list and click Next.
+   4. Now you get to choose whether you want to use DHCP (Automatic IP) or manually enter your network IP information (Manual Configuration). DHCP is the easiest choice. If you want to manually enter everything, I am going to assume that you know your IP information.
+   5. Your next screen will look different, depending on your choice of DHCP or manual configuration. In either case, you have a few self-explanatory check boxes to complete. The defaults are good if you aren’t sure what to choose.
+   6. Your next step is to optionally enter a hostname for your computer. After you click Next, there is a choice to enter a Zeroconf hostname. Zeroconf is a new network protocol that is trying to cut through the current tangle of proprietary protocols to make networking more simple. You are probably not using this, but it doesn’t hurt to retype your computer name in this box and click Next.
+   7. You are asked whether you want to restart your network. Of course you do. Yes. This action restarts the network service.
+   8. Read the happy Congratulations screen and click Finish.