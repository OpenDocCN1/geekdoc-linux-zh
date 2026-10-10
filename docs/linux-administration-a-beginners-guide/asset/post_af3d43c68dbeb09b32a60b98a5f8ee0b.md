
## Linux on the Rescue: A Story

At a site where we worked not too long ago, I had to deal with a somewhat bizarre printing situation. Two printers spook AppleTalk only. One spoke TCP/IP, but its Windows drivers were unstable and Macintosh users couldn’t get to it. Linux came to the rescue: I using Samba as an interface to Windows, and Netalkalsk as an interface to Macintosh users, all users pointed to a single server. Beneath the top layer were all the protocol conversion scripts to do the ugly tasks such as converting Windows-based requests to UNIX print requests, which fed into an AppleTalk converter. But in the end, printing was uniform across all platforms and all users could access all printers. This is the magic of configuration!

## The Registry vs. Text Files

I think of the Windows NT Registry as the ultimate configuration database—thousands upon thousands of entries, very few of which are completely documented, some located on servers and some located on clients.

“What?” Did you say your Registry got corrupted? “maniacal laughter” Well, yes, we can try to restore it from last night’s backups, but then Excel starts acting funny and the technician (who charges $50 just to answer the phone) said to re-install...

If you’re not getting my message, I’m saying that the Windows NT Registry system is, at best, very difficult to manage. Although it’s a good idea in theory, I’ve never emerged without injury from a battle with the Registry.

Linux does not have a “registry.” This is both a blessing and a curse. The blessing is that configuration files are most often kept as a series of text files (think of the Windows .INI files before the days of the Registry). This setup means you’re able to edit configuration files using the text editor of your choice rather than tools like regedit. In many cases, it also means you can literally comment those configuration files so that six months from now you won’t forget why you set something up in a particular way. In Linux, most configuration files exist in the /etc directory or one of its subdirectories.

The curse of a no-registry arrangement is that there is no standard way of writing configuration files. Each application or server can have its own format. Many applications are now coming bundled with GUI-based configuration tools. So you can do a basic setup easily, and then manually edit the configuration file when you need to do more complex adjustments.

In reality, having text files to hold configuration information usually turns out to be an efficient method. Once set, they rarely need to be changed; even so, they are straight text files and thus easy to view when needed. Even more helpful is that it’s easy to write scripts to read the same configuration files and modify their behavior accordingly. This is especially helpful when automating server maintenance operations, which is crucial in a large site with many servers.

## Domains

For a group of Windows NT systems to work well together, they should exist in a domain. This requires a dedicated NT Server system configured as a Primary Domain Controller (PDC). Domains are the basis of the Windows NT security model.

The basis of Linux's network security model is NIS, Network Information Service. NIS is a simple database (based on text files), which is shared with client workstations. Each primary NIS server (which by the way, does not require a complete dedicated system as a PDC usually does) establishes a domain. Any client workstation wanting to join this domain is allowed to do so, as long as it can set its domain name. To set the domain name, you must use the root user—Linux's equivalent to an Administrator user. Being part of the domain does not, however, immediately grant you rights that you would otherwise not have. The domain administrator must still add your login to the master NIS password list so that the rest of the systems in the network recognize your presence.

The key difference between NIS and NT domains is that the NIS server by itself does not perform authentication the way a PDC does. Instead, each host looks up the login and password information from the server and compares it to the user's entered information. It's up to the individual application to properly authenticate a user. Thankfully, the code necessary to authenticate a user is very trivial.

Another important difference is that NIS can be used as a general purpose database and thus hold any kind of information that needs to be shared with rest of the network. (This usually includes mount tables for NFS and e-mail aliases.) The only limitation is that each NIS map can only have one key, and the database mechanism doesn't scale well beyond about 20,000 entries. Of course, a site with 20,000 users shouldn't keep them all in a single NIS domain, anyway!

A final note about NT domains and NIS: Neither is required for the base operating system to work. Nevertheless, they are key if you need to maintain a multi-user site with a reasonable level of security.

## OTHER REFERENCES

If you are interested in getting under the hood of the technology revolution (and it's always helpful to know how things work), I recommend the following texts:

- *Computer: A History of the Information Revolution*, by Martin Campbell-Kelly and William Aspray. (Harper Collins, 1997)
- *A Quarter Century of Unix*, by Peter Salus. (Addison-Wesley, 1994)

Neither of these texts discusses Linux specifically. *A Quarter Century of Unix* does tell the Unix history up to the point where the system was just becoming a serious player. Peter Salus writes an interesting discussion of why Linus Torvalds saw a need to create Linux in the first place.

To get the scoop on Linux itself, start with the Linux home page at http://www.linux.org.

## SUMMARY

In this chapter we covered three important topics: Linux distributions, the GNU license (GPL), and the major design differences between Windows NT and Linux. You should now have a sharper picture of what lies ahead.

Linux is a very powerful operating system, capable of many things. Perhaps its most important feature is its configurability—it’s almost like silly putty! You can mold it into anything from basic to the most complex shapes. And breaking it is not easy to do. Be sure to keep this in mind as you read the remainder of this book and when you start working with Linux in any environment. Before letting yourself fall into the trap of believing that you have to get the feature you want from Uncle Bill [Gates], take a quick trip to the World Wide Web and find out if there isn’t in fact a project already in existence that will solve your problem.

Linux isn’t just a productive, efficient operation system; it also gives you a chance to think creatively. This author, for instance, has managed to keep his home Windows free for two years now. In fact, the initial draft of this book is being written in a Linux-based word processor.

# CHAPTER 2

# Installing Linux in a Server Configuration

# Linux Administration: A Beginner's Guide

A key attribute in Linux’s recent success is the remarkable improvement in installation tools. What once was a mighty frightening process many years back has now become almost trivial. Even better, there are many ways to install the software; CD-ROMs (although still the most common) are no longer the only choice. Network installations are part of the default list of options as well, and they can be a wonderful help when installing a large number of hosts.

> NOTE: “The version of Red Hat Linux 6.1 that ships with this book is the “Publishers Edition.” This means Red Hat had to make a special effort to get all of the package’s source code in addition to their easy-to-install format onto a single CD. As a result, some of the lesser used packages have to be dropped. For the complete list, look at the README_publishers-edition file located in the root directory of the CD-ROM.”

Most default configurations where Linux is installed are already capable of becoming servers. This is unfortunate due to a slightly naïve design decision: being designed as a server means that machine serves everything! From disk services to printers to mail to news to ... it all turns out on the server. As we all know, the reality is that most servers are dedicated to performing one or two tasks, and any other installed services simply take up memory and drag on performance.

In this chapter, we discuss the installation process as it pertains to servers. This requires us to do two things: differentiate between a server and client workstation and streamline a server’s operation based on its decided functions.

We will go through this process for both Red Hat Linux and Caldera Linux.

## BEFORE INSTALLATION

Before getting into the actual installation phase, it is important that we take a moment and evaluate two things:

- The hardware the system going to run on.
- The server’s ideal configuration to provide the services you need.

Let’s start by examining hardware issues.

## Hardware

As with any operating system, we should determine what hardware configurations will work before getting started with the installation process. Each commercial vendor publishes a hardware compatibility list (HCL) and makes it available on its Web site. Be sure you obtain the latest version of the lists so that you are confident in the hardware selected. In general, most popular Intel-based configurations work without difficulty; (Red Hat’s Web site is at http://www.redhat.com/hardware, and Caldera’s HCL is at http://www.calderasystems.com/products/openlinux/hardware.html.)
