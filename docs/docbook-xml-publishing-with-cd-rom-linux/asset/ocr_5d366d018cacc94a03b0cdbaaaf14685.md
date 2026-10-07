# Chapter 5: Making Online Documents

Instead, the OLink element contains LinkMode, LocalInfo, and TargetDocEnt attributes that help it return a value. The OLink element need not always point to the same target within the document or URL. The OLink element is designed to be used with dynamic content.

The LinkMode attribute points to the ModeSpec element, which is declared in the DTD of the document. The ModeSpec element describes an application to resolve OLinks, such as a search query against a database or other dynamic values.

The LocalInfo attribute provides information to the method used by the ModeSpec element. For example, if the ModeSpec element was a SQL query against a MySQL database, the LocalInfo attribute could supply the names of the tables or fields to search, or it could contain keywords to search. The ModeSpec element could be an interface for searching Google or any of the Web-based search engines, or it could query your parts database or pass a value to a PHP script.

The TargetDocEnt attribute value contains information used to resolve the OLink.

The OLink element is beyond the scope of this chapter; it is a rarely used element, though useful in integrating DocBook with other applications. For more information on the OLink element, see Appendix B.

# E-Mail

After you've completed your masterpiece and sent it into the world, you can include your e-mail address and receive the adoration and thanks from your readers via e-mail. (If you're really lonely, you can include your phone number using the Phone element, but that's another chapter.)

Seriously, though, you will usually want to include your e-mail address to get feedback on your document, updates, or error corrections. Also, you might want to include someone else's e-mail address if you're writing an article or document that contains information about others.

Whatever the reason, it's probably going to come up at some point. Including the e-mail address is easy. Just use the following syntax:

```
<para>
```

To send the author compliments, comments, and declarations of love and adoration, use the following email address: