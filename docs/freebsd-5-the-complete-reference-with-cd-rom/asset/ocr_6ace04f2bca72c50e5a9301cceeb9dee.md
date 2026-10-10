```
&lt;P&gt;&lt;IMG SRC="logo.jpg" ALT="Our Logo" ALIGN="LEFT" WIDTH="200"  
HEIGHT="150"&gt;&lt;/P&gt;

&lt;BR CLEAR=ALL&gt;

&lt;P&gt;Copyright &amp;copy; 2002.&lt;/P&gt;

&lt;/BODY&gt;
&lt;/HTML&gt;
```

# Features in this listing include

+   ■ **Document type** The `<!DOCTYPE>` tag begins most HTML files. Most web browsers work fine if it's omitted, but it's an important component because it identifies the version of the HTML standard that the file contains (4.01 in the case of Listing 20-1).

+   ■ **&lt;HTML&gt; tag** This tag identifies the beginning of a block of HTML code. It's mirrored at the very end of the file with a `</HTML>` tag.

+   ■ **&lt;HEAD&gt; tag** HTML files typically include two parts: a *header*, which contains meta-information such as the document's title, and a *body*, which contains the bulk of the text that displays in the web browser. The `&lt;HEAD&gt;` and `&lt;/HEAD&gt;` tags surround the header.

+   ■ **&lt;TITLE&gt; tag** This tag and its closing `</TITLE>` tag surround the document's title. Most web browsers display this title in their title bars.

+   ■ **&lt;BODY&gt; tag** This tag begins the body of the document, which ends with the `</BODY>` tag near the end of the file. The `&lt;BODY&gt;` tag includes additional optional parameters, which set the background color (BGCOLOR="#FFFFFF", which sets the background to white) and the text color (TEXTCOLOR="#000000", which sets the color to black). Pages that use background images also set them in the `&lt;BODY&gt;` tag, with the BACKGROUND="*filename.ext*" option.

+   ■ **&lt;CENTER&gt; tag** Many tags affect formatting. This tag tells the browser to center the text that ends with the `</CENTER>` tag. Similarly, the `RIGHT&gt;` and `LEFT&gt;` tags cause text to appear flush right or flush left, respectively. These tags, and especially the `&lt;CENTER&gt;`, are not used or needed by most modern browsers; instead, codes within other tags, such as header tags, accomplish these goals. Listing 20-1 includes a `&lt;CENTER&gt;` tag because it does no harm on modern browsers and makes the document slightly more portable.

+   ■ **Header tags** The `<H1>` tag is a header tag, which denotes a text heading, like the ones in this book. Use these to help organize a web page with more than a few paragraphs. (Its use in Listing 20-1 is unnecessary except as a demonstration of how it *can* be used.) Listing 20-1's `<H1>` tag includes an ALIGN="CENTER"