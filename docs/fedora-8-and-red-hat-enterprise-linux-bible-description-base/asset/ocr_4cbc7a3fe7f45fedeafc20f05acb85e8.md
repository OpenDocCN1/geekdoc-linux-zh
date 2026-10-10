among links. Then press Enter to go to the current link. Use the right and left arrow keys to go forward and back among pages you have visited. Press Esc to see a menu bar of features to select from.

While links doesn’t allow you to display images inline, if you select an image it will be displayed on your desktop in gThumb image viewer (by default). You also have the option of saving the image to your local hard disk.

+   - lynx — The lynx browser has a good set of help files that come with it (press the ? key). Step through pages using the Spacebar. Although lynx can display pages containing frames, it cannot display them in the intended positioning. Use the arrow keys to display the selected link (right arrow), go back to the previous document (left arrow), select the previous link (up arrow), and select the next link (down arrow).

As with links, lynx lets you display a selected image. However, lynx uses ImageMagick instead of gThumb to display the image you choose.

+   - w3m — The w3m text-based Web browser can display HTML pages containing text, links, frames, and tables. It even tries to display images (that feature has improved a lot in recent releases). There are both English and Japanese help files available (press H with w3m running). You can also use w3m to page through an HTML document in plain text (for example, `cat index.html | w3m -T text/html`). Use the Page Up and Page Down keys to page through a document. Press Enter on a link to go to that link. Press the B key to go back to the previous link. Search forward and back for text using / and ? keys, respectively.

> **NOTE:** You must install the elinks package to get links, the lynx package to get lynx, and the w3m package to get w3m. All of them are included with Fedora.

The w3m command seems the most sophisticated of these browsers. It features a nice default font selection, seems to handle frames neatly, and its use of colors also makes it easy to use. The links browser lets you use the mouse to cut and paste text.

You can start any of these text-based Web browsers by giving it a filename, or if you have an active connection to the network, a Web address. For example, to read the w3m documentation (which is in HTML format) with a w3m browser, you can type the following from a Terminal window or other shell interface:

```
```sh
$ w3m /usr/share/doc/w3m-0*/doc/MANUAL.html
```
```

An HTML version of the W3M Manual is displayed, or you can give w3m a URL to a Web page, such as the following:

```
```sh
$ w3m www.handsonhistory.com
```
```

After a page is open, you can begin viewing the page and moving around to links included in the page. Start by using the arrow keys to move around and select links. Use the Page Up and Page Down keys to page through text.