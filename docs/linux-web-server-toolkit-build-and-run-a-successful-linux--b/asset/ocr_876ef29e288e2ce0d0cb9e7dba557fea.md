# Linux Web Server Toolkit

the browser can't determine what the link points to. The link won't appear correctly, and the rest of the document may not appear at all, as the browser searches for the end of the <A> tag.

# UNDERSTANDING RELATIVE AND ABSOLUTE FILE LOCATIONS

You may have noticed a difference in the URLs used for links in the previous examples: one used a complete URL starting with http:// while the other started with the path to the filename /doc/manual_index.html.

Whenever you specify a filename, including a URL for a Web server, you can use an *absolute* or a relative description of the location for that file. An absolute URL includes the complete server and pathname (starting with http://). If any part of that complete server is left off [as in the previous example where the link starts with /doc], the browser must determine the complete URL by adding the missing parts, relative to the current document, and the Web server from which the document came. The distinction between absolute and relative filenames can cause problems; it's easy to get confused. Here are your choices for any tag parameter that requires a pathname and file, or a URL (for the <A> tag or the <IMG> tag):

+   * The path for a filename can be relative to the document root (where all other Web pages are stored) by starting with a forward slash like the first example above, or this <IMG> tag example.

```
<IMG SRC= /graphics/logbanner.gif >
```

This allows you to move the entire document to another server without having to edit the tags. But if someone copies them to a non-Web system, they must reside in the root directory or the links won't point to the right files.

+   * The path for a filename can be relative to the document in which a reference appears, not by starting with a forward slash. The image file in the following example must be in the same directory on the Web server as the document in which this tag appears:

```
<IMG SRC= yellow_ball.gif >
```

This allows the most flexibility, since Web documents can be moved anywhere, so long as the relationship between them is maintained (such as all graphics stored in a subdirectory called IMAGES that is one level below where all documents are stored).

+   * The path can be absolute, with a complete URL given to be displayed, in this example. (Absolute links are best in <A> tags that link to a document on another server. If you use them to link to documents on your own server, or for <IMG> tags, you can't move files around without editing your links.)