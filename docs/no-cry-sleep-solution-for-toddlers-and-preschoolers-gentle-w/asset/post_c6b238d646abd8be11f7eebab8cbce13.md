
The applications specified will depend on those available on your particular system. The MIME type is separated from the application with a semicolon. In many cases, X Window System-based programs are specified. Comments are indicated with a #. A * used in a MIME subtype references all subtypes. The entry image/* would be used for an application that can run all types of image files. A formatting code, %s, is used to reference the attachment file that will be run on this application. Sample mailcap entries are shown here. The first entry associates all image files with the xv image viewer. The next two associate video and video MPEG files with the xanim application.

```
image/*; xv %s
video/*; xanim %s
video/mpeg; xanim %s
```

You can also create and edit MIME types on the GNOME and KDE desktops. For GNOME, use the GNOME Control Center’s MIME types capplet. This capplet will list the MIME types defined for your system along with their associated filename extensions. Edit an entry to change the application and icon associated with that MIME type, that type of file. On KDE, use the KDE Control Center’s File Association entry under KDE Components. This will list MIME types and their associated filename extensions. Select an entry to edit it and change the applications associated with it. KDE saves its MIME type information in a separate file called mimelink in the KDE configuration directory.

Though you can create your own MIME types, a standard set already is in use. The types text, image, audio, video, application, multipart, and message, along with their subtypes, have already been defined for your system. You will find that commonly used file extensions such as .tif and .jpg for TIFF and JPEG image files are already associated with a MIME type and an application. Though you can easily change the associated application, it is best to keep the MIME types already installed. The current official MIME types are listed at the IANA Web site (www.iana.org) under the name Media Types, provided as part of their Assignment Services. You can access the media types file directly on their site.

## Evolution

Evolution is the primary mail client for Red Hat. It is installed by default along with OpenOffice. Though designed for GNOME, it will work equally well on KDE. Evolution is an integrated mail client, calendar, and address book, currently being developed by Ximian. The Evolution mailer is a powerful tool with support for numerous protocols (SMTP, POP, and IMAP), multiple mail accounts, and encryption. With Evolution, you can create multiple mail accounts on different servers, including those that use different protocols such as POP or IMAP. You can also decrypt PGP- or GPG-encrypted messages.

## GNOME Mail Clients: Evolution, Balsa, and Others

Several GNOME-based mail clients are under development, many of which you can currently use (see Table 13-2). These include Evolution, Balsa, Mahogany, Althea, MMC, SMAN, Pygmy, Spruce, and Sylpheed (Balsa, Evolution, and Sylpheed are included with Red Hat). Check the GNOME Web site for more mail clients as they come out. Many are based on the GNOME mail client libraries (camel) currently under development, which provides support for standard mail operations. Balsa is a GNOME mail client with extensive features, though it can operate under any window manager, including KDE, as long as GNOME is installed on your system. Evolution is an integrated mail client, calendar, and contact manager from Ximian. The Mahogany mail client is a GNOME mail client that also has versions for other platforms. Althea is a stable IMAP mail client. The SMAN simple mail client is used to access POP3 servers. Pygmy is a simple GNOME mail client written in the Python programming language that supports attachments and MIME message. Sylpheed is a mail and news client with an interface similar to Windows mail clients. Spruce is a GNOME e-mail client with support for multiple accounts. Several support tools are also available like mail checkers and notifiers, include RePopApp and Flink mail checkers, along with Sonicmail and gpostman mail notifiers.

| Application | Description |
|---|---|
| Balsa | E-mail client for GNOME that supports POP3, IMAP, local folders, and multithreading |
| Evolution | Ximian integrated mail client, calendar, and contact manager |
| Sylpheed | Mail and news client similar to Windows clients |
| Althea | Stable IMAP mail client |
| SQmail | A folder-based e-mail system (using mysql) |
| SMAN | Simple mail user agent that accesses POP3 servers |
| RePopApp | GNOME mail checker with support for multiple accounts |
| Mahogany | Cross-platform e-mail application |
| Flink | GNOME mail checker with IMAP, POP3, and mbox support |
| Pygmy | GNOME mail client written in the Python programming language |
| Spruce | E-mail client with support for multiple accounts |
| gpostman | Basic GNOME mail notifier |
| MMC | GNOME mail client |
| Sonicmail | GNOME POP3 mail notifier applet |

TABLE 13-2 GNOME Mail Clients
