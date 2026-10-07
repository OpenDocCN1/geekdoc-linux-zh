# Installing the DTDs and Stylesheets

If, for some reason, you already have a set of DTDs, but you're not sure whether you have the XML or SGML DTDs, check the filenames. Most DocBook XML filenames have an xml in them to identify them as XML. For instance, the main DocBook SGML DTD filename is docbook.dtd; the XML DTD is named docbook.xml.

Note that none of the DocBook files indicate which version number of DocBook they are. If you have more than one version of the DTDs floating around, be sure to put them in separate folders.

# Installing the DTDs and Stylesheets

When you have the files containing the DocBook DTD and stylesheets, you put them into their own directory. If you downloaded them from the DocBook site, copy the ZIP file into a directory. Unzip it with WinZip if you're on Windows or with unzip if you're on Linux or a UNIX-type operating system.

It doesn't matter where you put the DocBook directory and files. Some popular locations on UNIX-type operating systems are under the /usr/local

> Because the world is a fast-moving place, I'm including notes on how to install the DocBook DTD here. It's quite likely that the time this book is written and the time it is published, a new version of the DocBook DTDs will become available. However, to make life simple, I've included the DocBook DTDs in three package formats for easy installation on Linux systems. You can find packages on the CD-ROM in tgz format, the Red Hat Package Manager format, and the Debian package format. One of these should work on your system. I'll also try to keep updated install packages on my site, at http://www.ZonkerBooks.net/.

Hopefully, you won't need these instructions. However, it's good to have them. Check the README files in the directories for installation instructions for the Linux packages.

![](bbox=[0.835, 0.788, 0.91, 0.888])

For Windows users, you might want to place them under C:\docbook\sgml\ or C:\docbook\xml\, depending on which version you're using.