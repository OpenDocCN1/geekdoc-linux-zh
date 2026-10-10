# **Command-Line Tools**

If you're not working with a graphical desktop client environment, you'll need to use the Linux command-line tools to set the network configuration information. Quite a few command-line tools are at your disposal. The following sections cover the ones you're most likely to run into (and that you'll likely see on the Linux+ exam).

# **Network Manager Command-Line Tools**

The Network Manager tool also provides two different types of command-line tools:

+   - nmtui provides a simple text-based menu tool.
+   - nmcli provides a text-only command-line tool.

Both tools help guide you through the process of setting the required network information for your Linux system. The nmtui tool displays a stripped-down version of the graphical tool where you can select a network interface and assign network properties to it, as shown in Figure 7.3.

# **FIGURE 7.3** The Network Manager nmtui command-line tool

![](bbox=[0.24, 0.45, 0.77, 0.74])

The nmcli tool doesn't attempt to use any type of graphics capabilities; it just provides a command-line interface where you can view and change the network settings. By default, the command displays the current network devices and their settings, as shown in Listing 7.4.