the entire CrossOver Office product for $39.95 U.S.), the CrossOver Plugin lets you play some content that you could not otherwise use in Linux. (Download a demo from www.codeweavers.com/site/products/download_trial.)

After you install the CrossOver Plugin, you see a nice Plugin Setup window that lets you selectively install plug-ins for QuickTime 6, Windows Media Player 6.4, Shockwave 8.5, Flash 6, and Microsoft Word, Excel, and PowerPoint viewers. (Support for later versions of these content formats may be available by the time you read this.) You can also install other multimedia plug-ins, as well as a variety of fonts to use with those plug-ins.

> TIP: Although I have had CrossOver Plugin running fine in earlier versions of Red Hat Linux, at the time of writing it was not yet working in the current version of Fedora Core. Check with CodeWeavers to see if they have corrected CrossOver Plugin to run in the latest version of Fedora Core.

# Adding a Preferences toolbar

Did you ever run into a Web page that required you to use a particular type or version of a browser or had fonts or colors that made a page unreadable? The Mozilla preferences toolbar called PrefBar2 lets you try to spoof Web sites into thinking you are running a different browser. It also lets you choose settings that might improve colors, fonts, and other attributes on difficult-to-read pages.

You can install the neat little toolbar from the Mozdev.org site (prefbar.mozdev.org). Click the Install link; then, after it is installed, restart Mozilla.

> TIP: You must have write permissions to /usr/lib/mozilla-1.7.3 for the Install link to work. This may require you to log in as root, start Mozilla, install the Preferences Toolbar, and then log out as root.

The default set of buttons let you do the following:

+   * **Colors** — Change between default colors and those set on the Web page.
+   * **Images** — Toggle between having images loaded or not loaded on pages you display.
+   * **JavaScript** — Allow or disallow JavaScript content to play in Mozilla Navigator.
+   * **Clear Cache** — Deletes all cached content from memory and disk.
+   * **Kill Flash** — Kills all embedded Flash content on the current page.
+   * **Real UA** — Choose to have your browser identified as itself (current version of Mozilla) or any of the following: Mozilla 1.0 (in Windows 98), Netscape Navigator 4.7 (in Macintosh), Netscape 6.2 (in Linux), Internet Explorer 5.0 (in Macintosh), or Internet Explorer 6.0 (in Windows XP).

The user agent (UA) setting is very useful when dealing with Web sites that require Internet Explorer (IE) (and usually IE on Windows, not MacOS. The IE 6.0 WinXP setting is good enough to allow Mozilla to log on to the Microsoft Exchange webmail service, which is