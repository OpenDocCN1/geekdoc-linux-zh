
# Part II: Using Fedora and RHEL

Using the Preferences window (select Edit -> Preferences, and then click the Security button), you can manage certificates under the Encryption Tab. Select View Certificates to display a window that lets you import new certificates or view certificates that are already installed. Firefox will help check certificates that you encounter are valid (and warn you if they are not). See Chapter 14 for more information on using certificates.

Along with the excellent security features built into Firefox, it's important that you incorporate good security practices in your web browsing. Download and install software only from sites that are secure and known to you. For any online transactions, make sure you are communicating with a secure site (for the https protocol in the location box and closed lock icon in the lower-right corner of the screen). Be careful about being redirected to another Web site when doing a financial transaction. An IP address in the screen where you enter credit card information are warning signs that you may have been directed to an untrustworthy site.

Because new exploits are discovered all the time, it is important that you keep your browser up to date. This means that, at least, you need to get updates of Firefox as they become available (see Chapter 5 for information on using yum and PackageKit to get the latest software). To keep up with the latest security news about Firefox and other Mozilla products, refer to the Mozilla Security Center (http://www.mozilla.org/security).

# Tips for using Firefox

There are so many nice features in Firefox, it's hard to cover all of them. Just to point you a few mean and useful features, there are some extra tips that Firefox you might enjoy:

- **Add smart keywords** — Many Web sites include their own search boxes to allow you to look for information on their sites. With Firefox, you can assign a smart keyword to any search box on the Web, and then use the keyword from the location bar in the Firefox browser to search that.

  For example, go to the Linux Documentation Project site (http://tldp.org). Right-click in the Search/Resources box. Select Add Keyword for this Search from the menu that appears. Add a name (Linux Documentation) and a keyword (tldp) and select Add to the keyword to your Bookmarks.

  After you have added, you can use it by simply entering the keyword and one or more terms in the Firefox location box (on the navigation toolbar). For example, entered tldp Lego Mindstorms and came up with a list of HOW-tos for using Lego Mindstorms in Linux. This list comes as if you visited the site and typed in the text Lego Mindstorms into that site.

- **Check config** — Firefox has hundreds of configuration preferences available to set as you please. You can see those by typing about:config into the location box. For true/false options, you can simply click the preference name to toggle between the values. For other preferences, click the preference to enter a value into a pop-up box.
  While many of these values can be changed through the Preferences menu (Edit -> Preferences), some technical people prefer to look at settings in a list like the one shown on the about:config page. The about:buildconfig page lists the options used to build.

- **Multiple home pages** — Instead of having one home page, you can have a whole set of home pages. When you start Firefox, a separate tab will open in the Firefox window for each address you identify in your home page list. To do this, create multiple tabs (File -> New Tab) and enter the address for each page you want in your list of home pages. Select Edit -> Preferences -> Main and use the Current Pages bottom. The next time you open Firefox, it will start with the selected tabs open to the home pages you chose. (Clicking the Home icon will open new tabs for all the home pages.)

There are many more things you can do with Firefox than I have covered in this chapter. If you have questions about Firefox features or you want to dig up some more cool stuff about Firefox, I recommend checking out the Mozilla forum (http://forums.mozilla.org/viewforum.php?id=38). There is a sticky link to Miscellaneous Firefox forums and a quick FAQ.

# Using text-based browsers

If you become a Linux administrator or power user, you will inevitably find yourself working on a computer from a remote login or there is no desktop GUI available. At some point while you are in that state, you will probably want to check an HTML file or a Web page. To solve the problem, Fedora and RHEL will include several text-based Web browsers.

With text-based browsers, any HTML file available from the Web, your local file system, or a computer where you are remotely logged in can be accessed from your shell. There's no need to fire up your GUI or read pages of HTML markup if you just want to take a peek at the contents of a Web page. Besides letting you call up pages, move around with pages, some of these text-based browsers even display graphics right in a Terminal window!

Which text-based browser you use is a matter of which you are more comfortable with. Browsers that are available:

- **links** With links (package), you can open a file or a URL, and then traverse links from the pages you open. Use search (/string) and back (?string) to find text strings in pages. Use up and down arrows to go forward and back among links. Use the right and left arrow keys to go forward and back among pages you have visited. Press Esc to see a menu bar of features to select

While links doesn't allow you to display images, in gThumb if you select an image it will be displayed on your desktop in gThumb image viewer (by default). You also have the option of saving the image to your local hard disk.

- **lynx** — The lynx browser has a good set of help files that come with it (press the ? key). Step through pages using the Spacebar. Although lynx can display pages containing frames, it cannot display them in the intended positioning. The arrow keys to display the selected link (right arrow), go back to the previous document (left arrow), select the previous link (up arrow), and select the next link (down arrow).

With links, lynx lets you display a selected image. However, lynx uses ImageMagick instead of gThumb to display the image you choose.

- **w3m** — The w3m text-based browser can display HTML pages containing text, links, frames, and tables. It tries to display images (that feature has improved a lot in recent releases). There are both English and Japanese help files (press H with w3m running). You can also use w3m to page an HTML document in plain text (for example, cat index.html | w3m -T text/html). Use the Page Up and Down keys to page through a document. Press Enter on a link to go to that link. Press the B key to go back to the previous link. Search forward and back for text using / and ?, respectively.

> NOTE: You must install the elinks package to get links, the lynx package to get lynx, and the w3m package to get w3m. All of them are included in Fedora.

The w3m command seems the most sophisticated of these browsers. It features a default font selection, to handle frames nicely, and use of colors also makes it easy to use. The links browser lets you use the mouse to cut and paste text.

You can start any of these text-based browsers by giving it a filename, or if you have an active connection to the network, a Web Address. For example, to read the w3m documentation (which is in HTML format) with a w3m browser, you can type the following from a Terminal window or shell interface:

```
$ w3m /usr/share/doc/w3m-0*/doc/MANUAL.html
```

An HTML version of the W3M Manual is displayed, or you can give w3m a URL to a Web page, such as the following:

```
$ w3m www.handsonhistory.com
```

After a page is loaded, you can begin viewing the page and moving around to links included in the page. Start by using the arrow keys to move around and select links. Use the Page Up and Down keys to page through text.

# Communicating with E-mail

Running close second to Web browsers is the e-mail reader (referred to in network standards as a Mail User Agent, or MUA). Evolution is the recommended e-mail client for Fedora and RHEL. However, Thunderbird is the new kid on the block of e-mail clients.
