| Mail Client | Description |
| :--- | :--- |
| Kontact (KMail, KAddressbook, KOrganizer) | Includes the K Desktop mail client, KMail; integrated mail, address book, and scheduler |
| Evolution | E-mail client |
| Balsa | GNOME mail client |
| Thunderbird | Mozilla group stand-alone mail client and newsreader |
| Netscape | Web browser-based mail client |
| GNU Emacs and X Emacs | Emacs mail clients |
| Mutt | Screen-based mail client |
| Sylpheed | Gtk mail and news client |
| Mail | Original Unix-based command line mail client |
| SquirrelMail | Web-based mail client |

**Table 13-1** Linux Mail Clients

# MIME

*MIME* (the term stands for *Multipurpose Internet Mail Extensions*) is used to enable mail clients to send and receive multimedia files and files using different character sets such as those for different languages. Multimedia files can be images, sound clips, or even video. Mail clients that support MIME can send binary files automatically as attachments to messages. MIME-capable mail clients maintain a file called **mailcap** that maps different types of MIME messages to applications on your system that can view or display them. For example, an image file will be mapped to an application that can display images. Your mail clients can then run that program to display the image message. A sound file will be mapped to an application that can play sound files on your speakers. Most mail clients have MIME capabilities built in and use their own version of the **mailcap** file. Others use a program called metainfo that adds MIME support. MIME is not only used in mail clients. As noted in Chapters 6 and 7, both the KDE and GNOME file managers use MIME to map a file to a particular application so that you can launch the application directly from the file.

# The mime.types File

Applications are associated with binary files by means of the **mailcap** and **mime.types** files. The **mime.types** file defines different MIME types, associating a MIME type with a certain application. The **mailcap** file then associates each MIME type with a specific application. Your system maintains its own MIME types file, usually */etc/mime.types*.

Entries in the MIME types file associate a MIME type and possible subtype of an application with a set of possible file extensions used for files that run on a given kind of application. The MIME type is usually further qualified by a subtype, separated from the major type by a slash. For example, a MIME type image can have several subtypes such as jpeg, gif, or tiff. A sample MIME type entry defining a MIME type for JPEG files is shown here. The MIME type is image/jpeg, and the list of possible file extensions is "jpeg jpg jpe":

image/jpeg jpeg jpg jpe