# # CREATING WEB CONTENT

Configuring the Web server is the first step in running a Web site. The second step is to create useful and meaningful content. The default content in the Apache document root is documentation written by the Apache Group and IBM.

There are as many, or more, options for creating content than there are options available for configuring Apache. The first of these is simple files containing HTML. HTML is useful for sharing static information in an intuitive way. When the data to be displayed is dynamic, server-side includes, the Common Gateway Interface, Java, JavaScript, Java, or another server-side language extension must be employed. The subject of Web content can be only briefly touched on here, but the following chapter sections should give you a basic framework for deciding what is possible.

# ## HTML Documents

Begin by creating a hypertext document as the focal point to your service. This document, called a home page, can be created using a standard editor. The format, links, and programmatic characteristics of the document are specified using Hypertext Markup Language (HTML). HTML tags are special ASCII character sequences that are embedded within the text of the document. HTML tags take on one of three basic forms:

```
<tag-name> text </tag-name>
<tag-name attribute-name=arg> text </tag-name>
<tag-name>
```

HTML tags are not case sensitive; thus, `<TITLE>` is equivalent to `<title>`. A sampling of HTML tags is listed in Table 18-2.

A basic HTML document will have a title, one or more headings, text paragraphs, and optionally programmatic interfaces like links, lists, images, or input/output fields. The title field identifies the purpose of the document and is usually displayed separate from the document by most browsers. This means you will want to echo the title information using a heading within the document body. Six levels of heading fields are available. Text within the document is contained by paragraph tags. If you want custom formatting within a paragraph, you must use additional tags to honor the formatting. Generally, line breaks and spacing are ignored.

It's very easy to build and test HTML documents. Create a document using an editor of choice and save it with the file extension .html (The _.html_ extension is a convention rather than a requirement.) Use the Open Local or Open File option of a browser such as Netscape or Mosaic to display the document on the screen. Repeat the process until the document has been refined to meet your expectations. It's a good idea to review your document with a couple of different browsers to validate that it has a common look and feel. You can make things even easier by using one of the WYSIWYG HTML editors or tool sets. These tools will validate and/or display HTML information during the edit process. Example 18-10 shows HTML code for a test page, test.html.