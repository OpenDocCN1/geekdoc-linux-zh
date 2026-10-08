# URL Addresses

An Internet resource is accessed using a Universal Resource Locator (URL). A URL is composed of three elements: the transfer protocol, the hostname, and the pathname. The transfer protocol and the hostname are separated by a colon and two slashes, ://. The *pathname* always begins with a single slash:

```
`transfer-protocol://host-name/path-name`
```

The *transfer protocol* is usually HTTP (Hypertext Transfer Protocol), indicating a Web page. Other possible values for transfer protocols are **ftp** and **file**. As their names suggest, **ftp** initiates FTP sessions, whereas **file** displays a local file on your own system, such as a text or HTML file. Table 14-1 lists the various transfer protocols.

The *hostname* is the computer on which a particular Web site is located. You can think of this as the address of the Web site. By convention, most hostnames begin with www. In the next example, the URL locates a Web page called **guides.html** on the **tldp.org** Web site:

```
`http://tldp.org/guides.html`
```

If you do not want to access a particular Web page, you can leave the file reference out, and then you automatically access the Web site's home page. To access a Web site directly, use its hostname. If no home page is specified for a Web site, the file **index.html** in the top directory is often used as the home page. In the next example, the user brings up the Red Hat home page:

```
`http://www.redhat.com/`
```

The pathname specifies the directory where the resource can be found on the host system, as well as the name of the resource's file. For example, `/pub/Linux/newdat.html` references an HTML document called **newdat** located in the `/pub/Linux` directory.

The resource file's extension indicates the type of action to be taken on it. A picture has a **.gif** or **.jpeg** extension and is converted for display. A sound file has an **.au** or **.wav** extension and is played. The following URL references a **.gif** file. Instead of displaying a Web page, your browser invokes a graphics viewer to display the picture. Table 14-2 provides a list of the more common file extensions.

```
`http://www.train.com/engine/engine1.gif`
```

| Protocol | Description |
|---|---|
| **http** | Uses Hypertext Transfer Protocol for Web site access. |
| **ftp** | Uses File Transfer Protocol for anonymous FTP connections. |
| **telnet** | Makes a Telnet connection. |
| **news** | Reads Usenet news; uses Network News Transfer Protocol (NNTP). |

**TABLE 14-1** Web Protocols