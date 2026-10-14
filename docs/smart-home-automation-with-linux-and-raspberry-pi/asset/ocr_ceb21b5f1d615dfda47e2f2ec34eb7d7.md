However, unlike minidlna, Rygel appears to wait until the whole directory has been scanned before beginning. So after executing:

rygel

there is plenty of time to get a coffee!

# XBMC

Naturally, behemoth media systems such as XBMC can work as a server as well as a renderer. This is an ideal solution if you have one main media box, with the others considered as subordinate (or slave) units that are not accessed concurrently. When an XBMC server is feeding additional renderers it may not have enough processing power left over to power its own local renderer, along with the other requests made of it, so using separate slaves is a viable solution.

Sharing XBMC content to other devices is straightforward, and requires only that you enable it under the heading of “Share video and music libraries through UPnP.” Depending on the version of XBMC, this is either under Settings ➤ Network ➤ Services (version 11, aka Eden), or Settings ➤ Services ➤ UPnP (version 12, aka Frodo). You can then discover the media from your controller as normal.

> > **Note**　XBMC is a non-free package, so users of some distributions (such as Debian) will need to add additional repositories to use this through their standard package manager.

On the Raspberry Pi, XBMC can be installed by using either a custom installation (of which three currently exist), or by adding it as standard package of the Raspbian distribution (www.raspbian.org/RaspbianXBMC). The installers can be found at:

+   - http://wiki.openelec.tv/index.php?title=Installing_OpenELEC_on_Raspberry_Pi
+   - www.raspbmc.com/wiki/user/os-x-linux-installation/
+   - http://xbian.org/download/

with more information given in Chapter 9. Although this combination of XBMC and Raspberry Pi is not the most perfect match when partnered with anything connected to USB (e.g., external drives and especially DVDs), a lot of work is being done in this area, so improvements are anticipated with breath a-bated!

# Renderers

Almost all traditional media players can be considered renderers. Whereas originally they were limited to replaying media from the local drive, this slowly expanded to handling files across a network (through Samba) and now to UPnP. Space permits me the opportunity to briefly cover just a few of these.

# VLC

As a stalwart of media playback, VLC has embraced almost every new technology. UPnP is no exception, and it is the easiest one to use when verifying a newly configured UPnP server.

First, head the Tools ➤ Preferences menu. From here, select “All” to get the full tree view of configuration options. You can then open the Playlist branch and tick the “Universal Play n Play” option in the “Services and Discovery” section. You have now enabled UPnP on VLC.