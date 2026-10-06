# Part II: Using Fedora and RHEL

+   - lynx — The lynx browser has a good set of help files that come with it (press the ? key). Step through pages using the Spacebar. Although lynx can display pages containing frames, it cannot display them in the intended positioning. The arrow keys to display the selected link (right arrow), go back to the previous document (left arrow), select the previous link (up arrow), and select the next link (down arrow).

With links, lynx lets you display a selected image. However, lynx uses ImageMagick instead of gThumb to display the image you choose.

+   - w3m — The w3m text-based browser can display HTML pages containing text, links, frames, and tables. It tries to display images (that feature has improved a lot in recent releases). There are both English and Japanese help files (press H with w3m running). You can also use w3m to page an HTML document in plain text (for example, cat index.html | w3m -T text/html). Use the Page Up and Down keys to page through a document. Press Enter on a link to go to that link. Press the B key to go back to the previous link. Search forward and back for text using / and ?, respectively.

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