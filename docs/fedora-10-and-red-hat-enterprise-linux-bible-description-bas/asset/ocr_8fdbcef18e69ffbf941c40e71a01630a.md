# Part II: Using Fedora and RHEL

You can see that the document begins and ends with HTML tags &lt;html&gt; and &lt;/html&gt;. The beginning part of the Web page is contained within the &lt;head&gt; tags. The body of the page is contained within the &lt;body&gt; tags. The title of the page is set apart by title tags.

Between the beginning and ending body tags, you can add all kinds of stuff. You can have different types of bulleted or numbered lists. You can have headings, and text. More complex pages can include forms, dynamic HTML (which changes the content as you move or select items), or data special. Figure 9-2 shows an example of a Web page as it appears in Firefox.

![](bbox=[0.131, 0.259, 0.715, 0.555])

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