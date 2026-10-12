# ## Web pages

If you look at the HTML source code that produces Web pages, you see that it consists of a combination of information and markup tags, all of which are in plain-text format. The idea was to have Web pages be very portable and flexible. You can create a Web page with vi, emacs, Notepad, or any text editor on any computing platform. Or simplified front-end programs can be used to provide WYSIWYG (What You See Is What You Get) interfaces that let you see what you are creating as you go.

HTML tags are set apart by right and left angle brackets. Tags come in pairs, with a beginning tag, followed by information, and then an ending tag. The beginning tag contains the tag name, whereas an ending tag contains a forward slash (/) and the tag name. A minimal HTML page includes the following code:

```
<HTML>
<HEAD>
<TITLE>Greetings from Washington</TITLE>
</HEAD>
<BODY>
Here we are in beautiful Gig Harbor.
</BODY>
</HTML>
```

You can see that the document begins and ends with HTML tags (`<HTML>` and `</HTML>`). The beginning part of the Web page is contained within the HEAD tags. The body of the page is contained within the BODY tags. The title of the page (which appears in the browser’s title bar) is set apart by TITLE tags.

Between the beginning and ending BODY tags, you can add all kinds of stuff. You can have different types of bulleted or numbered lists. You can have headings, images, and text. More complex pages can include forms, dynamic HTML (which changes the content as you move or select items), or special data. Figure 9-1 is an example of a Web page as it appears in Netscape Communicator.

Some of the HTML code that was used to create the Web page shown in Figure 9-1 is as follows. The title of the Web page appears between two TITLE tags.

```
<TITLE>Swan Bay Folk Art Center - American Crafts
in Port Republic, NJ</TITLE>
```