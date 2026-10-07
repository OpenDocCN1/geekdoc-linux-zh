# Chapter 6: Parsing DocBook

You must also set up the ISO Entity sets for either SGML or XML. If you're using a Linux or UNIX-type system, the SGML ISO Entity sets are likely already there. If not, you can find them on the CD-ROM. As mentioned earlier, the XML Entity sets are available on the DocBook site, as well as on the CD-ROM for this book.

# The Easy Way Out

One of the things my Dad taught me was to look for the easiest way to do something and get the right result. Whether that means finding the easiest way to cut a piece of lumber or do something on the computer, I took that bit of advice to heart.

If you're in an office or company with a large number of users who are going to be creating DocBook documents and rendering output from them, installing DocBook and all the appropriate tools on each computer may not be the answer.

If you happen to have an older computer laying around, a Pentium or Pentium II computer with a 3 or 4 GB hard drive, at least 64 MB of RAM, and an Ethernet card, you can turn it into a DocBook processing monster.

Any Linux distribution is sufficient, but I'd recommend Debian/Linux for this task—and here's why: Debian is a wonderful package management tool called the Advanced Package Tool (APT). It makes installing any program that's been packaged for Debian a snap, especially DocBook's DTD and all of the requisite tools to create DocBook documents, including PSGML.

You'll find plenty of installation and usage information for Debian at http://www.debian.org/doc/

Once you have Debian installed, you probably have SGMLtools for the DocBook DTDs installed. If not, it's easy to do.

You should have a file called sources.list in the /etc/apt/ directory. Log in as root and edit that file to contain a line like this:

```
deb ftp://ftp.us.debian.org/debian stable main non-free
```

This line should be appropriate for anyone in the United States. It tells the apt-get program where to check for packages—in this case, the FTP server ftp.us.debian.org—and to check the stable distribution of Debian for