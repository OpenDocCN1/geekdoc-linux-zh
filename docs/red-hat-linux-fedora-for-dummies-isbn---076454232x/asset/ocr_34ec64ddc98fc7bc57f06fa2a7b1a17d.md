# Confidential for Windows users

If you're installing Red Hat Linux in a dual boot configuration with Windows NT, Windows 2000, or Windows XP, your NT boot record is temporarily overwritten, which means that you can't boot Windows NT. Don't panic: Your NT partition isn't erased — it has just been rendered unbootable. (An NT *boot record* is what enables a Windows NT system to start automatically when you start your computer.)

You can install Red Hat Linux without overwriting the NT boot partition if you click the *Change Boot Loader* button and select the *Do Not Install a Boot Loader* radio button. When you click the *Next* button, the *Advanced Boot Loader Configuration* window opens. Select the *First Sector of Boot Partition* option and then click the *Next* button. Your Windows boot configuration continues to operate as before.

![](bbox=[0.14, 0.4, 0.2, 0.46])

In the following section, we show you how to configure your network for Red Hat Linux use. If you don't have a network or just don't want to haggle with it right now, you may want to read the following section anyway because it makes your life easier if you decide to create a network sometime in the future. If you're still not interested, click *Next* and skip to the section after that, “Installation Stage 4: Configuring Your System.”

# Installation Stage 3: Configuring Your Network

If you're ready to configure your network and your computer has an Ethernet or Wi-Fi (a wireless network interface using the 802-11b standard) adapter, enter the appropriate information, as described in the following steps. If you have a network adapter but don't have a network to connect to, you should still enter a host name in Step 3. Entering a host name makes life easier down the line if and when you eventually connect to a network.

![](bbox=[0.14, 0.74, 0.2, 0.8])

Sometimes, the installation process doesn't detect a network device and skips the steps described in this section. If that happens, continue with the installation as described in the following section, “Installation Stage 4: Configuring your System.” You can configure your network after you finish installing Red Hat Linux. See Chapter 7 for network configuration instructions.

If you pick up from the end of the preceding section, the Network Configuration window appears. Follow these steps to configure your system for a network:

+   1. If you're *connecting to a network that uses the Dynamic Host Configuration Protocol* (DHCP), you don't have to do *anything more* to configure your network connection. Click the *Next* button and skip to *Step 7*.