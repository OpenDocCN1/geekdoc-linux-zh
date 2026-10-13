
## Table 12-3: Multimedia Applications

| Application | Description |
|---|---|
| GTV | GNOME MPEG video player |
| Xine | Multimedia player for video, DVD, and audio |
| GNOME-tv | TV tuner |
| aKtion | KDE video player |
| Kscd | Music CD player |
| Kaboodle | A media player |
| GNOME CD Player | CD Player |
| GNOME Sound Recorder | Sound recorder |
| XMMS | CD Player |
| Xplaycd | Music CD player |
| Noatun | KDE multimedia player |
| Xanim | Animation and video player |
| RealPlayer | RealMedia and RealAudio streaming media ([www.real.com](www.real.com)) |
| KReateCD | KDE CD writing interface for cdrecord, mkisofs, and cdda2wav |
| KonCD | KDE CD burner and ripper |
| GNOME Toaster | GNOME CD burner |

## Video Applications

Several projects are under way to provide TV, video, DVD, and DTV support for Linux (see Table 12-4). The site [linuxdvb.org](linuxdvb.org) provides detailed links to DVD, digital video broadcasting (DVB), and multicasting. The site also provides downloads of many Linux video applications.

Access to current DVD and media players is provided at [dvd.sourceforge.net](dvd.sourceforge.net). Here you will find links for players like Movietime, Mplayer, VideoLan, Oggie, and Xine. The VideoLan project ([www.videolan.org](www.videolan.org)) offers network streaming support for most media formats, including mpeg4 and mpeg2. It includes a multimedia player, VLC, that can work on any kind of system. Xine is a multipurpose video player for Linux/Unix systems that can play video, DVD, and audio disks. See [xinehq.de](xinehq.de) for more information. For DVD transcoding and Divx support, check the DVD::rip project.

DVD development efforts were initially supported by the Linux Video and DVD Project (LiViD). The development of an open source DVD player has been hampered by the concerns and restrictions of the MPAA and their control over the DVD decoding software (an officially licensed player is under development). Information about efforts to develop Linux DVD software can be had at [www.opendvd.org](www.opendvd.org). None of the open source software hosted at SourceForge performs CSS decryption of commercial DVDs.

For KDE, several video applications are available or currently under development, including video players (aKtion and Noatun). Check [apps.kde.com](apps.kde.com) for downloads. Currently available or under development for GNOME are TV tuners (Gnomevision and Gnome-tv), a video player (Gnome-Video), and a video editor (trinity). Check [www.gnome.org](www.gnome.org).

## Table 12-4: Video and DVD Projects and Sites

| Projects | Sites |
|---|---|
| linuxdvb.org | Links to video, TV, and DVD sites: linuxdvb.org |
| Xine | Xine video player: xinehq.de |
| DVD players | dvd.sourceforge.net |
| VideoLan | Network multimedia streaming: www.videolan.org |
| DVD::rip | DVD transcoding and Divx software: www.exit1.org/dvdrip/ |

## Chapter 13: Mail and News Clients

### Overview

Your Linux system supports a wide range of both electronic mail and news clients. Mail clients enable you to send and receive messages with other users on your system or accessible from your network. News clients let you read articles and messages posted in a newsgroups, which are open to access by all users. This chapter reviews mail and news clients installed with Red Hat Linux.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_286_0.png)

## Mail Clients

You can send and receive email messages in a variety of ways, depending on the type of mail client you use. Although all electronic mail utilities perform the same basic tasks of receiving and sending messages, they tend to have different interfaces. Some mail clients operate on a desktop, such as KDE or GNOME. Others run on any X Window System managers. Several popular mail clients were designed to use a screen-based interface and can be started from only the command line. Other traditional mail clients were developed for just the command line interface, which requires you to type your commands on a single command line. Most mail clients described here are included in standard Linux distributions and come in a standard RPM package for easy installation. For Web-based Internet mail services, such as Hotmail, Lycos, and Yahoo, you use a Web browser instead of a mail client to access mail accounts provided by those services. Table 13-1 lists several popular Linux mail clients.

Mail is transported to and from destinations using mail transport agents. Sendmail and Smail send and receive mail from destinations on the Internet or at other sites on a network (see Chapter 24). To send mail over the Internet, they use the Simple Mail Transport Protocol (SMTP). Most Linux distributions, including Red Hat, automatically install and locally configure Sendmail for you. On starting up your system, having configured your network connections, you can send and receive messages over the Internet.

You can sign your e-mail message with the same standard signature information, such as your name, Internet address or addresses, or farewell phrase. Having your signature information automatically added to your messages is helpful. To do so, you need to create a signature file in your home directory and enter your signature information in it. A signature file is a standard text file you can edit using any text editor. Mail clients such as KMail enable you to specify a file to function as your signature file. Others, such as Mail, expect the signature file to be named .signature.

## Table 13-1: Linux Mail Clients

| Mail Client | Description |
|---|---|
| Kontact (KMail, KAddressbook, KOrganizer) | Includes the K Desktop mail client, KMail; integrated mail, address book, and scheduler |
| Evolution | Primary mail client for Red Hat |
| Balsa, Mahogany, etc. | GNOME mail clients (see Table 13-2) |
| Mozilla Mail | Web browser-based mail client |
| Netscape | Web browser-based mail client |
| GNUEmacs and XEmacs | Emacs mail clients |
| Mutt | Screen-based mail client |
| Sylpheed | Gtk mail and news client |
| Mail | Original Unix-based command line mail client |
| nmh | New Message Handler command line mail client |

## MIME

MIME (the term stands for Multipurpose Internet Mail Extensions) is used to enable mail clients to send and receive multimedia files and files using different character sets such as those for different languages. Multimedia files can be images, sound clips, or even video. Mail clients that support MIME can send binary files automatically as attachments to messages. MIME-capable mail clients maintain a file called mailcap that maps different types of MIME messages to applications on your system that can view or display them. For example, an image file will be mapped to an application that can display images. Your mail clients can then run that program to display the image message. A sound file will be mapped to an application that can play sound files on your speakers. Most mail clients have MIME capabilities built in and use their own version of the mailcap file. Others, like Elm, use a program called metamail that adds MIME support. MIME is not only used in mail clients. As noted in Chapters 6 and 7, both the KDE and GNOME file managers use MIME to map a file to a particular application so that you can launch the application directly from the file.

Applications are associated with binary files by means of the mailcap and mime.types files. The mime.types file defines different MIME types, associating a MIME type with a certain application. The mailcap file then associates each MIME type with a specified application. Your system maintains its own MIME types file, usually /etc/mime.types.

Entries in the MIME types file associate a MIME type and possible subtype of an application with a set of possible file extensions used for files that run on a given kind of application. The MIME type is usually further qualified by a subtype, separated from the major type by a slash. For example, a MIME type image can have several subtypes such as jpeg, gif, or tiff. A sample MIME type entry defining a MIME type for JPEG files is shown here. The MIME type is image/jpeg, and the list of possible file extensions is "jpeg jpg jpe":

```
image/jpeg jpeg jpg jpe
```

The applications specified will depend on those available on your particular system. The MIME type is separated from the application with a semicolon. In many cases, X Window System-based programs are specified. Comments are indicated with a # . A * used in a MIME subtype references all subtypes. The entry image/* would be used for an application that can run all types of image files. A formatting code, %s, is used to reference the attachment file that will be run on this application. Sample mailcap entries are shown here. The first entry associates all image files with the xv image viewer. The next two associate video and video MPEG files with the xanim application.

```
image/*; xv %s
video/*; xanim %s
video/mpeg; xanim %s
```

You can also create and edit MIME types on the GNOME and KDE desktops. For GNOME, use the GNOME Control Center's MIME types capplet. This capplet will list the MIME types defined for your system along with their associated filename extensions. Edit an entry to change the application and icon associated with that MIME type, that type of file. On KDE, use the KDE Control Center's File Association entry under KDE Components. This will list MIME types and their associated filename extensions. Select an entry to edit it and change the applications associated with it. KDE saves its MIME type information in a separate file called mimelink in the KDE configuration directory.

Though you can create your own MIME types, a standard set already is in use. The types text, image, audio, video, application, multipart, and message, along with their subtypes, have already been defined for your system. You will find that commonly used file extensions such as .tif and .jpg for TIFF and JPEG image files are already associated with a MIME type and an application. Though you can easily change the associated application, it is best to keep the MIME types already installed. The current official MIME types are listed at the IANA Web site (www.iana.org) under the name Media Types, provided as part of their Assignment Services. You can access the media types file directly on their site.

## Evolution

Evolution is the primary mail client for Red Hat. It is installed by default along with OpenOffice. Though designed for GNOME, it will work equally well with KDE. Evolution is an integrated mail client, calendar, and address book, currently being developed by Ximian. The Evolution mailer is a powerful tool with support for numerous protocols (SMTP, POP, and IMAP), multiple mail accounts, and encryption. With Evolution, you can create multiple mail accounts on different servers, including those that use different protocols such as POP or IMAP. You can also decrypt PGP- or GPG-encrypted messages.

The Evolution mailer provides a simple GUI interface, with a toolbar for commonly used commands and a sidebar for shortcuts. A menu of Evolution commands allows access to other operations. The main panel is divided into two panes, one for listing the mail headers and the other for displaying the currently selected message. You can click any header title to sort your headers by that category. Evolution also supports the use of virtual folders. These are folders created by the user to hold mail that meets specified criteria. Incoming mail can be automatically distributed to their particular virtual folder.
