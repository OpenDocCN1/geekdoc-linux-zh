Syntax: Header action header value

Context: Server config, virtual host, directory, per-directory access control file (.htaccess)

Override: FileInfo

The allowed actions are as follows:

| Action | What It Does |
|---|---|
| Set | Sets a header. If an old header with the same name existed, its value is changed to the new value. |
| Add | Adds a header. This can cause multiple headers with the same name when one or more headers with the same name exist. |
| Append | Appends the value to an existing header value. |
| Unset | Removes a header. |

For example, the following directive adds the Author header with the value "Mohammed J. Kabir":

```
Header add Author "Mohammed J. Kabir"
```

And the following line removes the same header:

```
Header unset Author
```

# mod_expires

The mod_expires module is not compiled in Apache by default. It lets you determine how Apache deals with Expires HTTP headers in the server's response to requests. Expires HTTP headers provide you with means for telling the client about the time when the requested resource becomes invalid. This is useful when documents are cached by the client and need to be requested again. Most smart clients determine the validity of a requested document by investigating the cached document's expiration time provided by Expires HTTP headers. This module enables you to control the settings of the Expires HTTP headers.

# ExpiresActive

The ExpiresActive directive enables or disables the generation of the Expires header. It does not guarantee that an Expires header will be generated. If the criteria are not met, no header is sent.