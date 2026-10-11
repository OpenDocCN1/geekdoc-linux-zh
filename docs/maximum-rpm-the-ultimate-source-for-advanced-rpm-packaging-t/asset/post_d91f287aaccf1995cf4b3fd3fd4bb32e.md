
Let's look at the next file:

```
-rw-r---r--   1  root  97  359354  Jul 18  06:05  rpm-2.2.2-1.src.rpm
```

This is the source package file for **RPM** version 2.2.2, release 1. Like the binary packages, the source package requires **RPM** to install; therefore, it cannot be used to perform an initial install of **RPM**. Let's see what else is here:

```
-rw-r---r--   1  root  97  122157  Jul 18  06:05  rpm-devel-2.2.2-1.axp.rpm
-rw-f---r--   1  root  97  51132  Jul 18  06:05  rpm-devel-2.2.2-1.i386.rpm
-rw-f---r--   1  root  97  54470  Jul 18  06:05  rpm-devel-2.2.2-1.sparc.rpm
```

These files are binary package files that contain the **rpm-devel** subpackage. The **rpm-devel** package contains header files and the **RPM** library and is used for developing programs that can perform **RPM**-related functions. These files cannot be used to get **RPM** running. That leaves two files:

```
-rw-rw-r--   1  root  97  278620  Jul 18  06:05  rpm-2.2.2-1.i386.cpio.gz
-rw-rw-r--   1  root  97  358943  Jul 18  06:05  rpm-2.2.2.tar.gz
```

The first file is a gzipped **cpio** archive of the files comprising **RPM**. After you uncompress the file, **cpio** can be used to extract the files and place them on your system. Note, however, that there is a **cpio** archive for the i386 architecture only. To extract the files, issue the following command:

```
# zcat file.cpio.gz | cd / ; cpio --extract
```

When you're actually issuing the command, *file.cpio.gz* should be replaced with the actual name of the **cpio** archive.

Note that the archive should be extracted using **GNU cpio** version 2.4.1 or greater. It may also be necessary to issue the following command prior to using **RPM**:

```
# mkdir /var/lib/rpm
```

The last file, *rpm-2.2.2.tar.gz*, contains the sources for **RPM**. Using it, you can build **RPM** from scratch. This is the most involved option, but it is the only choice for people interested in porting **RPM** to a new architecture.

## F.2. Where to Talk About RPM

As much as we've tried to make this book a comprehensive reference for **RPM**, there are going to be times when you'll need additional help. The best way to connect with others who use **RPM** is to try one of the mailing lists listed in the following sections.

### F.2.1. The rpm-list Mailing List

Red Hat Software, Inc., maintains a mailing list specifically for RPM. To subscribe to the list, it’s necessary to send a mail message to

```
rpm-list-request@redhat.com
```

On the message’s subject line, place the word subscribe. After a short delay, you should receive an automated response with general information about the mailing list.

To send messages to the list, address them to

```
rpm-list@redhat.com
```

As with other online forums, it’s advisable to lurk for a while before sending anything to the list. That way, you’ll be able to see what types of questions are acceptable for the list. Let the list’s name be your guide; if the message you want to send doesn’t have anything to do with RPM, you shouldn’t send it to rpm-list!

In general, the flavor of rpm-list is a bit biased toward RPM’s development, building packages, and issues surrounding the porting of RPM to other systems. If your question is more along the lines of “How do I use RPM to install new software?” consider reviewing the first half of this book and lurking on rpm-list a while first.

### F.2.2. The redhat-list Mailing List

The redhat-list mailing list is meant to serve as a forum for users of Red Hat Software’s Linux operating system. If your question concerns the use of RPM on Red Hat Linux, redhat-list is a good place to start. To subscribe, send a message to

```
redhat-list-request@redhat.com
```

On the message’s subject line, place the word subscribe. After a short delay, you should receive an automated response with general information about the mailing list. As with rpm-list, it’s best to lurk for a while before posting to the list.

To send messages to the list, address them to

```
redhat-list@redhat.com
```

### F.2.3. The redhat-digest Mailing List

Some people might find the number of messages on redhat-list more than they can handle. However, there is a digest version of the list available. Each digest consists of one or more messages sent to redhat-list. The digest is sent out when the collected messages reach a certain size. Therefore, a digest might have one very long message or 20 smaller ones. In either case, you’ll have the collected knowledge of the Red Hat Software development team and their many customers, delivered in one message.

To subscribe to `redhat-digest`, send a message to `redhat-digest-request@redhat.com`

On the message's subject line, place the word `subscribe`. After a short delay, you should receive an automated response with general information about the mailing list.

To send messages to the list, address them to `redhat-list@redhat.com`

As always, observe proper netiquette—lurk before you leap!

## F.3. RPM on the World Wide Web

Up-to-date information on RPM can always be found at the RPM Web site: `http://www.rpm.org/`

The site is completely dedicated to RPM, which makes finding things a snap. You can also try Red Hat Software's Web site: `http://www.redhat.com/`

This site's content changes frequently, so it's impossible to specify an exact URL for RPM information. However, the site is very well run and always has a comprehensive table of contents as well as a search engine.

## F.4. RPM's License

RPM is licensed under the GNU General Public License or, as it's more commonly called, the GPL. If you're not familiar with the GPL, it would be worthwhile to spend a few minutes looking it over. The purpose of the GPL is to ensure that GPLed software remains freely available. “Freely available” doesn't necessarily mean at no cost, although GPLed software is often available by anonymous FTP. The idea behind the GPL is to make it impossible for anyone to take GPLed code and make it proprietary. But enough preliminaries! The best way to understand the GPL is to read it:

# GNU GENERAL PUBLIC LICENSE
Version 2, June 1991

Copyright © 1989, 1991 Free Software Foundation, Inc.
675 Mass Ave, Cambridge, MA 02139, USA
Everyone is permitted to copy and distribute verbatim copies of this license document, but changing it is not allowed.

## Preamble

The licenses for most software are designed to take away your freedom to share and change it. By contrast, the GNU General Public License is intended to guarantee your freedom to share and change free software—to make sure the software is free for all its users. This General Public License applies to most of the Free Software Foundation’s software and to any other program whose authors commit to using it. (Some other Free Software Foundation software is covered by the GNU Library General Public License instead.) You can apply it to your programs, too.

When we speak of free software, we are referring to freedom, not price. Our General Public Licenses are designed to make sure that you have the freedom to distribute copies of free software (and charge for this service if you wish), that you receive source code or can get it if you want it, that you can change the software or use pieces of it in new free programs; and that you know you can do these things.

To protect your rights, we need to make restrictions that forbid anyone to deny you these rights or to ask you to surrender the rights. These restrictions translate to certain responsibilities for you if you distribute copies of the software, or if you modify it.

For example, if you distribute copies of such a program, whether gratis or for a fee, you must give the recipients all the rights that you have. You must make sure that they, too, receive or can get the source code. And you must show them these terms so they know their rights.

We protect your rights with two steps:

1. copyright the software, and
2. offer you this license which gives you legal permission to copy, distribute and/or modify the software.

Also, for each author’s protection and ours, we want to make certain that everyone understands that there is no warranty for this free software. If the software is modified by someone else and passed on, we want its recipients to know that what they have is not the original, so that any problems introduced by others will not reflect on the original authors’ reputations.

Finally, any free program is threatened constantly by software patents. We wish to avoid the danger that redistributors of a free program will individually obtain patent licenses, in effect making the program proprietary. To prevent this, we have made it clear that any patent must be licensed for everyone’s free use or not licensed at all.

The precise terms and conditions for copying, distribution and modification follow.
