
2. Now, right-click the Network Manager icon on the top panel, and make sure that Enable Networking and Enable Wireless are checked (Figure 21-12). If they aren’t, check them, and wait a minute or two while the wireless card wakes up.

3. If the Enable Wireless option was already checked, try unchecking it, waiting for a minute or so, and then checking it again. Your wireless card might have needed turning off and on again to wake it up. You can also try doing this with the hardware switch/keyboard toggle I mentioned in Step 1.

4. If none of this has any effect, try restarting your computer. Some wireless cards work fine until you hibernate or suspend the computer, after which they fall into a deep sleep. Restarting should be enough to wake it up.

5. You should also check that the network you want to connect to doesn’t have a hidden network name (also called an SSID). If it does, it won’t appear in Network Manager’s list, you’ll have to manually enter its name to be able to connect. To do this, click the Network Manager icon, choose Connect to Hidden Wireless Network from the menu, and fill out the details in the window that appears.

6. Finally, if you’re still struggling, are you sure that you are sufficiently close to a wireless base station? If the signal is too weak, your card might not pick up the network at all.

![](img/f7cef0df22f9dba5a41777808c98eece_430_0.png)

Figure 21-12: Making sure that wireless and network connections are enabled in Network Manager

## Other Users on My Computer Can’t Connect

If you have more than one user account on your computer, you might find that you can connect to the Internet, but other users can’t. To fix this problem, you need to make your network connection available to all users:

- 1. While working in your user account, select System ▸ Preferences ▸ Network Connections.
- 2. Find the network connection that you use on one of the tabs. For example, if you use a wireless network called "Marconi," you would click the Wireless tab and look for Marconi in the list there.
- 3. Select the network, and click Edit.
- 4. Check the Available to all users option at the bottom of the screen, and click Apply.
- 5. Type your password when prompted. The network will disconnect, and you may need to reconnect it by using the Network Manager icon on the top panel (see Chapter 4 for further details on connecting).
- 6. Log in to a different user account. You should now be able to connect to the network in that user account too.

## Problems with the Display and Graphics Cards

Recently, Ubuntu has been doing an excellent job of detecting graphics cards, so it’s unlikely that you’ll ever be left staring at a blank screen. Things aren’t guaranteed to turn out perfect, however. This section covers such problems as getting 3D acceleration support (if it’s missing) and adjusting your screen resolution (if it’s looking weird). Just in case, there’s something to help you with a dreaded blank screen too.

### Games/Compiz Don’t Work: Installing Accelerated Graphics Drivers

If you can’t get Compiz or a certain game to work, you might need to install some accelerated graphics drivers. This is because only basic drivers (which can’t handle fancy effects and 3D games) are installed for some graphics cards by default, due to the lack of availability of suitable open source alternatives. If accelerated drivers exist for your card, you can install the more powerful (but possibly less open source) drivers by selecting System ▸ Administration ▸ Hardware Drivers, selecting the graphics driver from the list, and then clicking Activate to install it. Once it’s installed, restart the computer, and the new driver should be enabled.

You can directly download Linux graphics drivers from some manufacturers. These tend to be updated more regularly than the ones that come with Ubuntu, and they may have some extra features too. The next couple of sections cover how to get these drivers for the two biggest manufacturers, ATI and nVidia.

### ATI Cards

- 1. Go to http://support.amd.com/us/gpudownload/Pages/index.aspx/, and select Linux x86 from the list on the left side of the page.
- 2. Choose the type of card you have from the next list, and choose the model/series of your card from the list next to that.
- 3. Click GO!, and you’ll be taken to a download page for the driver. Scroll down to the bottom of the page, and click Download.
- 4. When prompted, click Save File to download the driver.
- 5. When the download finishes, find the driver file. It will probably be saved in your Downloads folder, and its name should end with .run.
