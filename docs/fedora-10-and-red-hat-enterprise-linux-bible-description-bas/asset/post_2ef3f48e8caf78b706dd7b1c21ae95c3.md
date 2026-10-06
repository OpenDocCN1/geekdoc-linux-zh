
# Part II: Using Fedora and RHEL

You can see that the document begins and ends with HTML tags `<html>` and `</html>`. The beginning part of the Web page is contained within the `<head>` tags. The body of the page is contained within the `<body>` tags. The title of the page is set apart by title tags.

Between the beginning and ending body tags, you can add all kinds of stuff. You can have different types of bulleted or numbered lists. You can have headings, and text. More complex pages can include forms, dynamic HTML (which changes the content as you move or select items), or data special. Figure 9-2 shows an example of a Web page as it appears in Firefox.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_411_0.png)

**Figure 9-2**: Many Web pages contain text, images, headings, and links.

Some of the HTML code that was used to create the Web page shown in Figure 9-2 is shown. The title of the Web page appears between two title tags:

```
<title>Swan Bay Folk Art Center - American Crafts in Port Republic, NJ</title>
```

The following code is used to create a link that opens a new mail message window:

```
<A HREF="mailto:webmaster@handsonhistory.com">Contact Us</a>
```

The text Contact Us is a link to an e-mail address. When someone clicks that link, a new message window appears, allowing person to send e-mail to that address.

```
<A HREF="bsched.htm">
New Basket Class!</A>
```

The words New Basket Class! point to a link to another HTML page. If someone were to click on those words, the bsched.htm page would appear.

You can find excellent resources on HTML at the World Wide Web Consortium (http://www.w3.org) and Html Goodies (http://www.htmlgoodies.com/).

# Browsing the Web with Firefox

Firefox web offers real competition to Microsoft Internet Explorer. Firefox is lightweight (it performs fast), includes many ease-of-use-features, and was built with a security priority. If you've switched to Fedora, you can get Firefox for Windows, Mac OS X, and other Linux systems. With the Fedora CD and DVD that come with this book, you can find Firefox out right now.

Firefox version 3 is offered in Fedora 10. This version features great improvements in performance, as well as new security, ease-of-use, and personalization features over previous releases.

Figure 9-3 shows an example of the Firefox Web browser:

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_412_0.png)

Figure 9-3: Firefox makes it easy to search, dubbed browsing, and get plugins in a secure way.

Because Firefox is the default browser for the current Fedora and RHEL, if you have one install that includes the desktop, Firefox should already be installed. (If it's not, you need to install the Firefox package from the Fedora DVD.) To start Firefox from your Fedora desktop, select the globe icon from your panel or select Internet -> Firefox Web Browser from the Applications menu has some of its best features available right in its main window (as shown in Figure 9-3). Here are some examples:

- **Tabbed browsing** — Instead of opening multiple windows to have several pages available at a time, Firefox includes a very efficient tabbed browsing feature. Select File -> New Tab (or by pressing Ctrl+T). Then type the URL for the new Web page you want. Figure 9-3 shows the Firefox window with two opening tabs. Tab options set from Preferences (Edit -> Preferences -> Tabs) can be set to automatically open new links in a new tab or open new links from other applications in a new tab. This can help preserve screen real estate by containing multiple pages in one window.

- **Live Bookmarks** — For sites that have RSS news and headlines available, a small RSS icon appears in the location of bar of the Firefox screen (see Figure 9-3). Using that icon, you can bookmark the advertised RSS feed to have headlines that can be displayed from your Bookmarks menu.

Try a site as `http://fedoraforum.org`. Click the RSS button. When prompted, choose Subscribe to Live Bookmarks for the site. Select Bookmarks, and select the bookmark. To the right of the bookmark, a list of articles available from the site appears. You can go straight to an article that interests you to. Or, you can choose Open in Tabs to open all the articles in separate tabs.

There are many sites that include RSS support these days. Try `trackers.com, cnn.slashdot.org, abcnews.com, cbsportsline.com` for other examples of sites that offer RSS news.

> NOTE: If you visit a site that you know is an RSS site, the headlines you see in XML code, means the page is not identifying itself as an RSS site. You can add a Live Bookmark for the site by selecting Bookmarks -> Subscribe to This Page. If Firefox recognizes the site as an RSS feed, it will display a Subscribe button at the top of the page. If this does not work, add the site as a normal bookmark. From the Library screen, select File -> Bookmark. When prompted, enter a name for the live bookmark, and then type (or cut and paste) the location of the RSS page into the Feed Location box and click OK. That new bookmark, and today's articles from that site, will appear on your Bookmarks list.

- **Using the sidebar** — Select View -> Sidebar to have Bookmarks or History appear as a sidebar in the Firefox window. Add your own bookmarks, return to pages from your history list, or use the Search box to search for content from those lists. Type Ctrl+B and Ctrl+H to toggle on and off Bookmarks and History sidebars, respectively.

# Chapter 9: Using the Internet and the Web 367

- **Web searches** — A box for designing keyword searches from Google is built right into the Firefox navigation toolbar. A drop-down menu lets you to search Yahoo!, Answers.com, Creative Commons, Amazon.com, and eBay. Or select "Manage Search Engines" from the drop-down list to go to the Firefox Search Engines page, where you can choose from more than 20 different engines.

- **Finding text** — Click Edit -> Find In This Page to open a toolbar at the bottom of the window for searching the current page for a text string. This allows you to search for the page text without having a little pop-up window in your way. After typing the text string, click Find Next or Previous to search for the string. You can also click Highlight to highlight all instances of the string on the page. As a shortcut, type a forward slash /, to display the Find toolbar.

- **Resizing text on web** — There is a new shortcut that lets you quickly resize the text on most web pages in Firefox. Hold the Ctrl and press the plus (+) (-) keys. The text on the web page (in most cases) gets larger or smaller, respectively. That page with the insanely small font is suddenly readable. (Remember to hold the Shift key to change a + character.)

- **Checking history** — Select History -> Show All the history appear on the Library screen. From that window, you can do keyword searches for sites you have visited, display the site names you have visited in various ways (by date, site name, most visited, and last visited), and browse through and revisit a site.

Some of the best features of Firefox are not near the surface. In particular, Firefox is designed for safe computing, so Firefox is very careful about what it will and not allow by default. Here are some important features of Firefox that can contribute to safety and fun web browsing:

- **pop-ups** — In Firefox, pop-up windows are blocked by default. To see and change how pop-ups are handled from Firefox, select Edit -> Preferences and select Content. The Block Pop-ups option is either selected (to block pop-ups) or unselected (to allow them). If pop-ups are blocked, you can click Exceptions to add sites from which you will allow pop-ups. JavaScript code in Web pages by clicking the Advanced button associated with the Enable JavaScript checkbox.

- **Advanced Security** — With Firefox, you have a lot of control over what content can be played and what software can be downloaded to your computer. You can view or change many security features from the Preferences window (select Edit -> Preferences). The Content tab you choose to enable Java or JavaScript, load images, or block pop-up windows.

If you have been using Firefox for a bit, while there are 3 new features you might find interesting. Inside Firefox 3 is the new Gecko 1.9 rendering
