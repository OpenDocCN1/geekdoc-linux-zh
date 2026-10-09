
## IndexOptions
Table 5-7 shows the options that you can use with `IndexOptions`.

| Option | What It Does |
|---|---|
| `FancyIndexing` | Turns on fancy indexing of directories. Note that the `FancyIndexing` and `IndexOptions` directives will **override each other** |
| `IconHeight[=pixels]` | Enables Apache to include the `HEIGHT=pixels` attribute in the `IMG` tag of the icon, which makes the loading of the icon faster on most browsers. If you do not specify a pixel count, a standard default is used. |
| `IconsAreLinks` | Makes the icons part of the anchor for the filename, for fancy indexing. |
| `IconWidth[=pixels]` | Enables Apache to include the `WIDTH=pixels` attribute in the `IMG` tag of the icon, which makes the loading of the icon faster on most browsers. If you do not specify a pixel count, a standard default is used. |
| `ScanHTMLTitles` | If you want Apache to read the title (denoted by the `<TITLE>` and `</TITLE>` tag pair) of an HTML document for fancy indexing, use this option. If you have already specified a description using the `AddDescription` directive, however, this option is not used. Note that reading each file’s content and searching for title information is a time-consuming task that may slow down the delivery of directory listings. I do not recommend this option. |
| `SuppressColumnSorting` | By default, Apache makes clickable column headers for a fancy directory index, which enables users to sort information in that column. This option disables this feature. |
| `SuppressDescription` | If you do not want to display file descriptions in the fancy directory listing, use this option. |
| `SuppressHTMLOreamble` | If the directory actually contains a file specified by the `HeaderName` directive, the module usually includes the contents of the file after a standard HTML preamble (`<HTML>`, `<HEAD>`, and so on). The `SuppressHTMLOreamble` option disables this behavior. |
| `SuppressLastModified` | Suppresses the display of the last modification date in fancy indexing listings. |
| `SuppressSize` | Suppresses the file size in fancy indexing listings. |

## IndexOrderDefault

The IndexOrderDefault directive enables you to change directory listing views by sorting various fields such as names, date, size, and description in directories that are displayed using the FancyIndexing feature.

- **Syntax:** IndexOrderDefault Ascending | Descending Name | Date | Size | Description
- **Context:** Server config, virtual host, directory, per-directory access control file (.htaccess)
- **Override:** Indexes

## ReadmeName

If you want to insert a file at the end of the fancy directory listing, use the ReadmeName directive.

- **Syntax:** ReadmeName filename
- **Context:** Server config, virtual host, directory, per-directory access control file (.htaccess)
- **Override:** Indexes

For example, the following makes Apache look for a file called readme.html (extension is assumed) or readme to insert at the end of the listing:

```
ReadmeName readme
```

## Response Header Modules

Apache allows you to send customer HTTP response header when sending data. The modules in this section, as shown in Table 5-8, enable you to configure various custom response headers.

Table 5-8 Response-Header Modules

| Module | Purpose |
| --- | --- |
| mod_alias | Send files that contain their own HTTP headers. |
| mod_headers | Add arbitrary HTTP headers to resources. |
| mod_expires | Apply Expires headers to resources. |
| mod_cern_meta | Support for HTTP header metafiles. |

### mod_asis

The *mod_asis* module is compiled by default. This module enables you to send a document as-is — in other words, the document is sent to the client without HTTP headers. This can be useful when redirecting clients without the help of any scripting. To send a file as is, you need to make sure that *httpd.conf* file contains an entry such as:

```
AddType httpd/send-as-is .asis
```

This assigns the MIME type *httpd/send-as-is* to file extension *.asis*. If you create a file called *foobar.asis* and a client requests it, the file is sent to the client without any HTTP header. It is your job to include appropriate headers in the file. For example, if you want to provide a redirect mechanism via the *.asis* files, you can create files with headers such as:

```
Status: 301 Text Message
Location: new-URL
Content-type: text/html
```

Listing 5-2 shows a file called *redirect.asis*, which redirects the clients to a new location.

Listing 5-2: *redirect.asis*

```
Status: 301 We have moved.
Location: http://www.our-new-site/
Content-type: text/html
<H1>Notice to Visitors</H1>
Please update your bookmark to point to <A HREF="http://www.our-new-site/ "> www.our-new-site/ </A><BR>
<BR>
Thanks.
```

When a client requests this file, the 301 status message tells the client to use the location information to redirect the request. You do not have to add the *Date:* and *Server:* headers, because the server automatically adds them. However, the server does not provide a *Last-Modified* header.

### mod_headers

This module is not compiled by default. *mod_headers* enables you to manipulate HTTP response headers, and it offers a single directive called *Header*, which enables you to manipulate the HTTP response header.

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

## mod_expires

The mod_expires module is not compiled in Apache by default. It lets you determine how Apache deals with Expires HTTP headers in the server's response to requests. Expires HTTP headers provide you with means for telling the client about the time when the requested resource becomes invalid. This is useful when documents are cached by the client and need to be requested again. Most smart clients determine the validity of a requested document by investigating the cached document's expiration time provided by Expires HTTP headers. This module enables you to control the settings of the Expires HTTP headers.

### ExpiresActive

The ExpiresActive directive enables or disables the generation of the Expires header. It does not guarantee that an Expires header will be generated. If the criteria are not met, no header is sent.

**Syntax:** *ExpiresActive* On | Off

**Context:** Server config, virtual host, directory, per-directory access control file (`.htaccess`)

**Override:** Indexes

### ExpiresByType

The *ExpiresByType* directive specifies the value of the *Expires* HTTP header for documents of a specified *MIME-type*. The expiration time is specified in seconds. You can define the time in two ways. If you choose to use the *Mseconds* format to specify expiration time, then the file’s last modification time is used as the base time. In other words, *M3600* means that you want the file to expire one hour after it was last modified. On the other hand, if you use the *Aseconds* format, then client’s access time is used as the base time. Following are some examples.

**Syntax 1:** *ExpiresByType* *MIME-type* *Mseconds* | *Aseconds*

**Syntax 2:** *ExpiresByType* *MIME-type* "*base_time* [plus] *num* *Years* | *Months* | *Weeks* | *Days* | *Hours* | *Minutes* | *Seconds*"

**Context:** Server config, virtual host, directory, per-directory access control file (`.htaccess`)

**Override:** Indexes

The following expires all plain-text files after one hour in the client’s cache:

```
ExpiresByType text/plain A3600
```

And the following expires all GIF files after one week from the last modified time:

```
ExpiresByType image/gif M604800
```

If you want to use the second syntax for specifying expiration times, you need to determine the appropriate value of *base_time* by using the following options:

| Value | What It Means |
| :--- | :--- |
| Access | Time when client accessed the file. |
| Now | Current time. This is the same as the access time. |
| Modification | Time when the file was last changed. |

For example, the following directives tell Apache to send headers to tell the browser that HTML documents should be expired after seven days from the day of access and that the GIF images should be expired after any changes in file or three hours and ten minutes later.
