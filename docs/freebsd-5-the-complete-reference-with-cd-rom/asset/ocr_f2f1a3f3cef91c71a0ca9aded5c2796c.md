option, which is the method most modern browsers use to center an element. Additional levels of heading are possible—`<H2>`, `<H3>`, and so on. Most browsers display these headings in varying fonts and font sizes, much as you see in books.

+   -   **Paragraph tags**
+       The `<P>` and `</P>` tags denote the starts and ends of paragraphs. Web browsers may rewrap text within the paragraphs, so you can place line breaks wherever you like. If you need to place information on a new line, you must surround it in these tags or use another tag, such as `<BR>` (described shortly).

+   -   **Links**
+       Web page *links* are specified with `<A HREF>` tags, which list the URL in quotes within the opening tag. (A bare `</A>` tag closes a link.) The text between the opening and closing tags appears as a link in the web page when viewed by a user, and if the user clicks or otherwise selects the link, an attempt is made to access the specified URL. You can specify any of several different protocols in the URL, such as another web page (`http://`), an FTP site (`ftp://`), or an e-mail address (`mailto:`).

+   -   **Emphasized text**
+       The `<STRONG>` and `<EM>` tags provide two means of emphasizing text. Most browsers use **bold** for `<STRONG>` and *italic* for `<EM>`, but this practice isn’t universal.

+   -   **Graphics**
+       The `<IMG>` tag specifies a graphic that’s to be displayed in the reader’s web browser. Listing 20-1 includes several options in this tag, the most important of which is `SRC`, which specifies the source of the file. This may be a filename alone (possibly including a relative path), in which case the client retrieves the image from the same server that delivered the main page; or a complete URL, in which case the image may reside on a different server entirely. The `ALT` option provides a brief textual description of the image, which may be important for visually impaired users and those who configure their browsers to not load graphics automatically. The `WIDTH` and `HEIGHT` options specify the size of the graphic in pixels, which allows browsers to display text before retrieving the graphic, or to scale the image to another size.

+   -   **`<BR>` tag**
+       This tag specifies a line break. The `CLEAR=ALL` option further specifies that the tag is to clear all intervening elements. The net result is that subsequent text appears after the graphic; without this tag, some browsers display the next paragraph to the right of the graphic.

+   -   **Special symbols**
+       Listing 20-1 includes only one special symbol, a copyright symbol, which is indicated by `&COPY;`. You may also want to use `&LT;` and `&GT;`, which denote less than (<) and greater than (>) symbols, which can’t be used directly because of their special meanings in specifying tags.

Most types of tags may be nested. For instance, you can create text that’s both bold and italic (on typical browsers’ displays) by using the `<STRONG>` and `<EM>` tags simultaneously:

```
<STRONG><EM>A very emphasized point!</EM></STRONG>
```