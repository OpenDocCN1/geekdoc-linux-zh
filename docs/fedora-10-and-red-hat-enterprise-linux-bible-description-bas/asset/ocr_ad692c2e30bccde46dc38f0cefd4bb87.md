# Chapter 9: Using the Internet and the Web 377

values. For other preferences, click the preference to enter a value into a pop-up box.
While many of these values can be changed through the Preferences menu (Edit -> Preferences), some technical people prefer to look at settings in a list like the one shown on the about:config page. The about:buildconfig page lists the options used to build.

+   **Multiple home pages** — Instead of having one home page, you can have a whole set of home pages. When you start Firefox, a separate tab will open in the Firefox window for each address you identify in your home page list. To do this, create multiple tabs (File -> New Tab) and enter the address for each page you want in your list of home pages. Select Edit -> Preferences -> Main and use the Current Pages bottom. The next time you open Firefox, it will start with the selected tabs open to the home pages you chose. (Clicking the Home icon will open new tabs for all the home pages.)

There are many more things you can do with Firefox than I have covered in this chapter. If you have questions about Firefox features or you want to dig up some more cool stuff about Firefox, I recommend checking out the Mozilla forum (http://forums.mozilla.org/viewforum.php?id=38). There is a sticky link to Miscellaneous Firefox forums and a quick FAQ.

# Using text-based browsers

If you become a Linux administrator or power user, you will inevitably find yourself working on a computer from a remote login or there is no desktop GUI available. At some point while you are in that state, you will probably want to check an HTML file or a Web page. To solve the problem, Fedora and RHEL will include several text-based Web browsers.

With text-based browsers, any HTML file available from the Web, your local file system, or a computer where you are remotely logged in can be accessed from your shell. There's no need to fire up your GUI or read pages of HTML markup if you just want to take a peek at the contents of a Web page. Besides letting you call up pages, move around with pages, some of these text-based browsers even display graphics right in a Terminal window!

Which text-based browser you use is a matter of which you are more comfortable with. Browsers that are available:

+   **links** With links (package), you can open a file or a URL, and then traverse links from the pages you open. Use search (/string) and back (?string) to find text strings in pages. Use up and down arrows to go forward and back among links. Use the right and left arrow keys to go forward and back among pages you have visited. Press Esc to see a menu bar of features to select

While links doesn't allow you to display images, in gThumb if you select an image it will be displayed on your desktop in gThumb image viewer (by default). You also have the option of saving the image to your local hard disk.