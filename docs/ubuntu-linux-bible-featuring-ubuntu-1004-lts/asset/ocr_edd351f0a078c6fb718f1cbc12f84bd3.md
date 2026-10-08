# Chapter 18: Consumer Electronics and Ubuntu

create a new one with the correct name, copy the entries from the old playlist to the new one, and then delete the old playlist.

+   - On iPods: An empty playlist named New playlist is simply added to the end of available playlists on your iPod. This is fine, because you can edit the names of playlists on an iPod. To rename a playlist on an iPod, right-click on its name in the left pane and select Rename from the pop-up menu that displays. You can then edit the name of the playlist in the left pane and press Enter/Return on your keyboard or click elsewhere to save the new name.

Once you have created a new playlist, click the name of the device on which you created it to see the songs that it contains. You can drag songs to the playlist by one, or use the techniques described in the tip earlier in this section to select and drag multiple songs at the same time.

# Disconnecting Your Audio Player

You should not simply disconnect a digital audio player from your computer system. There should actually be no problem in doing so if you have made any changes to its contents, but it's a good idea to be in the habit of using the Rhythmbox Eject command before connecting a digital audio player. Don't worry, this doesn't shoot your iPod across the room—the Eject keyword is shared with devices that you actually eject, such as CDs and DVDs. Using this command guarantees that all pending changes have been written to your digital audio device, removing any tracks that you selected for deletion.

To eject a digital audio player in Rhythmbox, right-click on the name of the device in the left pane and select Eject from the context-sensitive menu that appears. If you have made changes to the device, you will see a notice in the lower-right corner of your GNOME desktop stating that data must be written to the device before you remove it. When all data has been written to the device, another dialog opens stating that it is now safe to disconnect the device.

# Working with an iPod Using gtkpod

You may be wondering why I'm even bothering to discuss a separate application for working with audio files on the iPod, when Rhythmbox already does a great job. This is simply because that wasn't always the case—iPod support is a fairly recent addition to Rhythmbox. Since gtkpod has been around for years and offers some capabilities Rhythmbox does not, I don't think it's a great application for working with an iPod, especially if you don't like Rhythmbox. Feel free to skip this section—or read on if you're interested in reading about an excellent alternative to working with your iPod using the "standard" Ubuntu applications.

Since Rhythmbox is installed by default with iPods, the gtkpod application is not installed by default on Ubuntu systems. In order to follow along in this section, you'll have to use your favorite Package Management software (as discussed in Chapter 19, "Adding, Removing, and Updating Software") to install the gtkpod package.