
## How This Book Is Organized

This book is divided into seven parts ranging from two to five chapters each. Each section covers one set of topics that are closely related to one another. These parts are as follows:

- Part I, "Networking Principles," covers the basics of networking, including both hardware and software. If you’re planning a small network and aren’t already familiar with networking hardware, you should read this section to learn what hardware is best for your needs. Other chapters in this section introduce concepts that you’ll find useful in understanding the rest of the book.
- Part II, "Configuring Linux Networking," covers the basic configuration tasks you’ll need to perform other networking operations discussed in the book. These basic tasks include information on Linux configuration, recompiling a kernel, Ethernet networking, and dialup PPP connections to the Internet.
- Part III, "File Sharing," discusses how to use Linux in a file-sharing network. Individual chapters cover basic file sharing principles and each of three major file sharing protocols: NFS, SMB/CIFS, and AppleTalk. The focus in this section is on using Linux as a server, but I also cover using Linux as a client for each of these protocols except AppleTalk, for which Linux support is currently very preliminary and therefore unstable. This section also includes a chapter on backing up your network using Linux as a backup server.
- Part IV, "Printer Sharing," mirrors the organization of Part III, with sections on basic principles and printer sharing details for each of three major printer sharing protocols.
- Part V, "Remote Access," covers using your Linux computer from a distance. You can do so either using text-only tools or using tools that allow you to run X GUI programs from a distant computer. You can use this capability to make a central Linux computer function much like a mainframe of old, handling not just storage but processing; or for occasional remote access to your data and programs when you’re at home or travelling.
- Part VI, "Linking Your Intranet to the Internet," discusses two popular and important methods of using a Linux computer as a gateway between an internal network and an external one: IP masquerading and firewalking. The former lets you "hide" an entire network behind one computer so the outside world believes only one computer exists. The latter protects an internal network, but doesn’t necessarily mask the presence of those computers from the outside world.
- Part VII, "Final Considerations," covers three important topics that simply didn’t fit anywhere else: Hardware considerations when building a new computer; advanced system administration; and security concerns. Each of these topics is touched upon at various other points in the book, but deserves greater attention than was appropriate in chapters about other matters.

If you’re new to networking and want to get a good feel for the topic as a whole, you can read this book straight through. If you need information on specific topics, you can read the appropriate chapters, mostly in whatever order you like. Parts III and IV, though, each begin with a chapter that you’ll find helpful in understanding the material presented in subsequent chapters in their respective sections. When I think you might want more information on a topic, either as a prerequisite for understanding material or to learn more, I tell you where to look in this book, or in other books or on the Internet.

## What’s on the CD-ROM?

The CD-ROM that accompanies this book contains a copy of Red Hat Linux 6.0. This copy has had all the patches applied to it that Red Hat has released up to the date on which the CD was mastered, so you don’t need to apply these patches yourself. Red Hat will probably have released new updates between the CD mastering date and the time you read this, though, so you should still check Red Hat’s Web site and compare the version numbers of updated packages to what you have installed. The text file updates.txt on the CD includes information on both where to find updated packages and the updates that have been preapplied to the CD that comes with this book.

The subdirectory `sams-extras` includes most of the programs I discuss in this book that don’t come with a standard Red Hat Linux distribution. If you’re not using Red Hat Linux, you may want to check your own distribution’s CDs for equivalent packages before installing the ones that come with this book, but the packages I’ve included should be usable with most RPM-based Linux distributions. Some of the included programs do require glibc 2.1, though, and so might not work with older distributions, such as Red Hat 5.x.

Because you may want to read the CD from Windows as well as from Linux, it’s been created with both Joliet and Rock Ridge long filenames. You should, therefore, have no trouble getting to the relevant Windows files, or even Linux files if you need to, using Windows or any other OS that understands the Joliet filesystem.

## Conventions Used in This Book

This book uses certain conventions to help you get the most from the text.
