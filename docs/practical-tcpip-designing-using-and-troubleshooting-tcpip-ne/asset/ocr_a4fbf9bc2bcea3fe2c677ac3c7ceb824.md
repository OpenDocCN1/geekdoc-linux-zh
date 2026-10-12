/vnd.name is a vendor-specific subtype, indicating that the commercial product name should be used to process this. For example, **application/vnd.ms-excel** is how a Microsoft Excel spreadsheet is attached. (Microsoft Word documents are **application/msword** without the “vnd.” because this subtype was registered as a standard before the **vnd** convention existed.)

There are two further “composite” top-level media types. These are container-type items that require further processing by MIME itself to extract the sub-attachments from the container. Each sub-attachment is specified in the usual way, with its own MIME headers. These headers are most often used in the headers for the overall message, which is how MIME says there are attachments within.

+   6. **multipart**– data consisting of multiple entities. Subtypes are are:

+   /**alternative**: each of the body parts is an “alternative” version of the same information. This is used widely to send the same e-mail message in both HTML and plain text.

+   /**mixed** – the body parts are independent and their order is significant. We saw an example of this in Module 12.2, to indicate that the message contained a text part and a binary part.

+   /**digest** the body parts are a series of mail messages

+   7. **message** – a mail message within a mail message. Subtypes are:

+   /**rfc822** – a full mail message included as an attachment

+   /**partial** – one fragment of a larger message (which the mail client is expected to reassemble when all the fragments have been received).

You can have nested structures – attachments within attachments – using the composite content types (Appendix 14).

# Optional parameters

The optional parameters give further information about this attachment and are specified as name=value. For example,

**charset**=us-ascii specifies the character set as ASCII, which is the default, and may be omitted.

If the character set is anything else, it must be specified explicitly as a parameter in the Content-Type field, e.g,

```
Content-Type: text/plain; charset=ISO-8859-1
Content-type: text/plain; charset=Windows-1252
```

Other common parameters you will see frequently are “**boundary**=”, which specifies the string separating the parts of the body, e.g.

```
Content-Type: multipart/mixed; boundary=“____ main boundary ____”
```

and “**name**=”, giving the filename that an attachment originated from:

```
Content-Type: application/msword; name=“proposal.doc”
```

The **name** parameter is also used with the Content-Disposition header (Module 12.5).