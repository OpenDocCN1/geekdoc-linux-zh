
## 6.7 Future versions of Bodhi Linux

Like Windows, distros such as Ubuntu and Bodhi Linux bring out new versions every couple of years or so. The next major Ubuntu release is scheduled for April 2014, and the new Bodhi release (version 3.0) will come out a month or two after that.

You will not be able to update your existing Bodhi installation to version 3, instead you will have to do a fresh install - i.e. you will have to download the new disc image, install it on your computer, and repeat everything you have done in this guide. The good news is that there is no urgency about this: version 2 of Bodhi will be supported for a further couple of years.

When you do make the switch, you must obviously back up all your important data files first, as the hard disk on your computer will be reformatted. It might also be a good idea to back up your entire system onto an external hard disk or a (large) USB stick, as described above, just in case you need to run it again for any reason.

After that, minor revisions to the Bodhi distro will be released about three times a year, but these will be automatically incorporated into your installation when you do a `sudo apt-get dist-upgrade`.

## 6.8 Conclusion

We’ve reached the end this guide. You will have realized that there is much more to Bodhi and the Enlightenment desktop than is covered here, and as for Linux itself I’ve barely scratched the surface. Probably the best way to find out more about Linux is to search the web, including ‘ubuntu’ in your search phrase and sometimes ‘linux’. There are many guides available there. And as for Bodhi and Enlightenment, your main source of help will be the Bodhi website, especially the Forum and the Documentation Wiki.

I’ve replicated the customized Bodhi that’s described in this book, with all its tweaks and applications, on the computers of several acquaintances, and if you become a Bodhi convert you might do the same (using the USB stick or DVD you created in the last section). If so, you might find it useful to provide them with the Quick Start Guide below.

## Quick Start Guide to this Bodhi Linux installation

All the applications on this computer can be accessed via the menu system, which you can open by pointing the mouse at any exposed area of the desktop and clicking left.

This installation includes a number of shortcuts to make life easier:

- Frequently-used applications such as the web browser are located on the shelf at the left. Simply click on the appropriate icon to run these.
- Other favourite applications can be found on the Favorites menu, which is reached by pointing the mouse at a blank area of the desktop and clicking right.
- Keyboard shortcuts, such as Win + End to shut down the computer (i.e. hold down the Windows key and tap End).
- Mouse actions to manipulate windows:
  - Click the top-right corner of the screen to close the current (focused) window.
  - Click the top edge of the screen to maximize the window (click again to undo this).
  - Click the bottom edge of the screen to minimize the window.
  - Click the top left corner to set the window fullscreen (click again to undo).
  - Click the left edge of the screen to left-maximize the window (click again to undo).
  - Click the right edge of the screen to right-maximize the window (click again to undo).
  - Click the bottom-right corner of the screen to show the desktop.

The Nautilus file manager is included in this installation. Its icon is located at the top of the shelf. When Nautilus opens, you can press the F3 key to display a second pane; this simplifies the task of copying or moving files from one location to another (right-click the file and choose e.g. Copy to other pane). Nautilus also makes it easy to access other computers connected to your network - Choose Browse network in its left pane.

The applications installed on this system include Firefox web browser, Thunderbird email client, LibreOffice office suite (the Linux alternative to Microsoft Office), Osmo personal information manager (calendar, diary, notes, contacts, todo list), VLC video player, Audacious music player, an audio recorder, Mirage for photos, as well as Skype and Dropbox. You can add others by visiting the AppCenter at the Bodhi Linux website ([http://appcenter.bodhilinux.com/](http://appcenter.bodhilinux.com/)). If a package that you want isn’t listed here, search for it using the Synaptic Package Manager (on the Favorites menu).

The terminal is the second icon down on the shelf. Use this to enter any commands; in particular the commands to keep your system and its software up to date. To keep things easy, these commands have been simplified on this system, so all you have to do is:

1. Enter `update` to synchronize your system file index with the on-line database (you must be connected to the Internet for this and the next command to work).
2. Then enter `upgrade` to replace any out-of-date system files.

To learn more about the Bodhi Linux system, including how to access the Internet, click anywhere on the desktop to open the menu system, then highlight ‘Bodhi Linux’ and choose Quick Start.
