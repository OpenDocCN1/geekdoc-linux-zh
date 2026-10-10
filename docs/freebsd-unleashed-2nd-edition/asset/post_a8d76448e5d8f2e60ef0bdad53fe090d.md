
module's documentation the same way you'd specify it in a script. Listing 20.2 shows part of the documentation for the `Image::Size` module.

# **LISTING 20.2** Sample Documentation for a Perl Module

```
# perldoc Image::Size

Image::Size(3) User Contributed Perl Documentation Image::Size(3)

NAME

       Image::Size - read the dimensions of an image in several
       popular formats

SYNOPSIS

       use Image::Size;
       # Get the size of globe.gif
       ($globe_x, $globe_y) = imgsize("globe.gif");
       # Assume X=60 and Y=40 for remaining examples

       use Image::Size 'html_imgsize';
       # Get the size as "HEIGHT=X WIDTH=Y" for HTML generation
       $size = html_imgsize("globe.gif");
       # $size == "HEIGHT=40 WIDTH=60"

       use Image::Size 'attr_imgsize';
       # Get the size as a list passable to routines in CGI.pm
       @attrs = attr_imgsize("globe.gif");
       # @attrs = ('-HEIGHT', 40, '-WIDTH', 60)

       use Image::Size;
       # Get the size of an in-memory buffer
       ($buf_x, $buf_y) = imgsize($buf);
```

Documentation of this type will generally give you usable and accurate prototype code that you can insert into your scripts, as well as a complete listing of all available functions.

### Perl Modules and the Ports Collection

The "correct" way to install Perl modules is with the ports collection. Go into /usr/ports and look through the various subdirectories. You'll see many ports beginning with `p5-`. These are Perl modules that have been codified into proper FreeBSD ports. (Package versions of most of them exist, too.) Many modules have compiled C components as well as multiple supporting modules and documentation, so it's definitely important to make sure everything gets installed in the proper place. The ports make sure of that.

The port for Net::Telnet is `/usr/ports/net/p5-Net-Telnet`, and that's the naming scheme for all of them—a dash for the double colon. Some port categories have dozens of Perl modules, all of them added to the ports out of repeated usefulness. This distributed model allows Perl to be infinitely extensible while remaining fairly unencumbered in its default installation.

To install a module from the ports, simply build it as you would any port—using `cd` to change to its directory and then running `make` and `make install`. Perl modules have a built-in `make test` target that tunes and evaluates how well the module will work on the system; this is run implicitly with the ports' `make target`.

You can use `pkg_info` and `pkg_version` to check which Perl modules you have installed; this is much easier than remembering to look in `/usr/local/lib/perl5`. The rest of the package tools work as well; you can use `pkg_add` to install a Perl module from its tarball, if you like, and use `pkg_update` to refresh it when a new version comes out.

## Useful Perl Resources

Because Perl is so widespread, it's little wonder that there are so many resources for it available in as many formats as you might want. Nearly everyone involved in content provider work on the Internet needs to have some familiarity with Perl, so computer book-stores do a brisk trade in books on the subject, and the most curious or off-topic of searches on the Web will turn up discussions between Perl hackers on how to do this or that.

The following sections list some of the more centralized and “official” sources of Perl information.

### Web Sites

If you need a Perl reference, the first stop should be the Web. It's not as direct or definitive as a book, but if you don't have such a book, you're sure to find your answer on the Web in at least some form.

`www.perl.org`

`www.perl.org` is the “Perl Mongers” Web site, an independently run source of information and advocacy references. There are mailing lists you can join as well as affiliated Web sites, such as `www.perldoc.com`, the centralized Perl documentation database.

`www.perl.com`

The “official” Perl site, run by O'Reilly, is an aggregation of Perl news, tutorials, and discussions about all kinds of details of working with Perl. This is probably the most complete site for everyday Perl happenings, if not necessarily for definitive reference.

### Books

Just about every Perl hacker has one of the popular O'Reilly Perl reference books on hand; for complete and easy-to-follow reference, these books are hard to beat.

### The “Camel” Book

Programming Perl is the complete Perl reference book, written by Larry Wall (the father of Perl), Tom Christiansen, and Jon Orwant (O'Reilly, 2000). Nicknamed for the camel on the cover, which has become synonymous with Perl as a visual logo, this book is frequently revised to cover the most recent developments in the Perl world, and it's widely accepted as the “definitive” work on the subject. One of its best features is an alphabetized function reference, an indispensable section.

### The “Llama” Book

Learning Perl, by Randal L. Schwartz and Tom Phoenix (O'Reilly, 2001) is the “camel” book's little brother; the llama is its icon. It discusses the basics of Perl (essentially the same topics covered in this chapter) in enough detail and with an engaging-enough style to cover pretty much all you'll need to get you to where Perl is no longer a foreign language to you.

### Perl Developer's Dictionary

Perl Developer's Dictionary by Clinton Pierce (Sams, 2001, ISBN: 0672320673) is a comprehensive reference of all Perl functions, and one of the most complete texts on the subject available today. It's ideal for the more advanced Perl hacker who needs reference on syntax and usage more than tutorials on how Perl works.

### Teach Yourself Perl in 24 Hours

This step-by-step, entry-level guide also by Clinton Pierce (Sams, 2002, ISBN: 0672320355) gives you a running start into putting Perl to practical use very quickly. Also, Teach Yourself Perl in 21 Days (Sams, 2002, ISBN: 0672322765) takes the tutorial to the next level of depth with lots of concrete examples.

### The CPAN

The CPAN (Comprehensive Perl Archive Network) is where all the modules across the Net are pulled together and made public. This also applies to binary distributions, scripts, and other tools, as well as source code for the brave of heart. Its primary usefulness, though, is for its comprehensive module list; if there's a module you want to install that isn't in the ports collection, you'll find it here, as well as all kinds of documentation that will help you use it.

The CPAN's central site is at http://www.perl.com/CPAN-1ocal/. The CPAN's purpose is to provide numerous worldwide mirrors of its resources so that everyone will have quick access to it; you can use the site's list and map to find a mirror close to you and bookmark it for later reference.

## PART IV
## FreeBSD Networking

### IN THIS PART

- CHAPTER 21 Networking with FreeBSD 475
- CHAPTER 22 Configuring Basic Networking Services 507
- CHAPTER 23 Connecting to the Internet with PPP 525
- CHAPTER 24 Configuring E-mail Services 543
- CHAPTER 25 Configuring a Web Server 577
- CHAPTER 26 Configuring an FTP Server 609
- CHAPTER 27 Configuring an Internet Gateway 621
- CHAPTER 28 Configuring a Database Server 637
- CHAPTER 29 Network Security 681
- CHAPTER 30 Virtual Private Networks (VPNs) 727
- CHAPTER 31 The Domain Name Server 743
- CHAPTER 32 The Network Filesystem (NFS) 765
- CHAPTER 33 File and Print Sharing with Microsoft Windows 777
- CHAPTER 34 Dynamic Host Configuration Protocol (DHCP) 793

# CHAPTER 21
# Networking with FreeBSD

Operating systems used to be designed either for networking or for single-user desktop settings. That has all changed. In the present day, the consumer-level, single-user, non-networked PC platform is giving way to operating systems whose robustness and networkability put to shame many of the mainframe-class systems of the old days. Mac OS X (with its FreeBSD architecture and Mach kernel) and Windows 2000/XP are both examples of platforms that were built around networking as a fundamental tenet, and they are intended to replace older, formerly non-networkable systems. TCP/IP (the *de facto* transport protocol suite of the Internet) is woven tightly into the cores of these systems as it was in the mainframes, and as it is in FreeBSD.

FreeBSD is a system designed from the ground up to be a network-aware platform. Whether you're using it as a workstation or as a server, chances are you're using it for its networking strengths, and a FreeBSD machine without a network is frankly not a lot of use. It's certainly a great deal less fun.

In this chapter, you'll learn the basic principles of networking as it applies to FreeBSD and its role in the Internet.

## Introduction to Networking

Networking is the ability of two or more computers to be aware of each other's existence and exchange data. In the Internet age, this basic capability can mean anything from simple awareness sensing and topology mapping to e-mail traveling from server to server, Web browsers downloading HTML pages and large movie files from HTTP servers, and peer-to-peer MP3 sharing. A networked computer has the

### IN THIS CHAPTER

- Introduction to Networking
- Network Topologies
- Network Components
- Network Protocols
- TCP/IP
- IP Addresses
- Routing
- Hostnames and Domain Names
- The Dynamic Host Configuration Protocol (DHCP) and Automatic IP Addressing
