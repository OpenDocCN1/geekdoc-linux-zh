
Most importantly, a list of mirror sites for the Linux kernel sources. I say most importantly because when a new kernel release is made, it becomes next to impossible to connect to the Web site due to the high volume of traffic. Fortunately, there are mirrors galore for the Linux source code and if you are willing to wait a day or so, you can easily get the latest patch.

## FIGURE 2.7
The Linux Kernel Archives.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_71_0.png)

For more than just kernel source, a favorite site among Linux users is Kernelnotes, formerly known as LinuxHQ. This site maintains a plethora of information related to the Linux kernel, including

- Source code browsers for the latest stable and development branches of the kernel
- Patch summaries describing what new and wonderful features are available
- Pointers to patch repositories for patches that haven’t made it into the mainstream kernel yet

There are also lots of links to other sources of information including Alan Cox’s home page as maintainer of the old stable source tree; a mirror of the Linux Documentation Project pages; and archives of the various Linux mailing lists, including linux-kernel, where all of the key kernel developers hang out. You can visit this wonderful Web site at http://kernelnotes.com/ (see Figure 2.8).

## FIGURE 2.8
The Kernelnotes.org site.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_72_0.png)

## Linuxcare

Another invaluable resource to systems administrators of Linux systems is a relative newcomer in the Linux world, but is backed by some long-time Linux supporters. Linuxcare provides a range of services, including

- Technical support
- Education and training
- Consulting
- Open source development

In addition to these services, Linuxcare also maintains a searchable Linux knowledge base. They will also provide problem tracking for your Open Source project, and provide Linux forums in which you can participate. To top it off, Linuxcare is a Linux portal site providing the latest Linux news and information. Finally, you can find information on hardware that has been certified to run with Linux from major manufacturers such as Dell, Compaq, and IBM. You will find them on the Web at http://linuxcare.com/ (see Figure 2.9).

## FIGURE 2.9
The Linuxcare home page.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_73_0.png)

## Linux Today

One other Linux resource on the Web is the Linux Today site. This site does much of your Web surfing for you. It collects information from news sources all over the Web, including articles about Linux, security announcements, and new releases of the kernel. In addition to news postings, you can read original editorials from the Linux Today staff, as well as interact with the Linux community utilizing the feedback options. If you are looking for up-to-the-minute news about who is doing what with Linux, Linux Today is the place to look. In addition to the breaking headlines, Linux Today also provides a place to look for or post Linux-related jobs. Through its sister site, Linux PR, you can find press releases about Linux-related products or from companies that support Linux. Linux Today can be found on the Web at http://linuxtoday.com and Linux PR can be found at http://linuxpr.com. A sample of the type of information you can find at Linux Today can be seen in Figure 2.10, which shows their home page.

## FIGURE 2.10
The Linux Today home page.

![](img/4886c42c7629f445c7f7f3011ffbf3c3_74_0.png)

## Other Web Sites of Interest

The sites already mentioned are but a sampling of those that might be of use to the systems administrator. There is a wealth of other sites, both general purpose and specific to a particular facet of Linux. These sites are too numerous to mention, but here are a few of my personal favorites:

- http://www.slashdot.org/ Slashdot is where developers and systems administrators can come to discuss the technology news of the day.
- http://www.linux.com/ This is a portal site and contains a section of particular interest to administrators on system tuning.
- http://www.freshmeat.org/ Freshmeat is an excellent site at which to find the latest open source software and discuss it with the developer.

## Other Sources of Information

In addition to the resources found on the Web, the Internet has much more to offer to the Linux community. Some of these resources include FTP sites that carry software for Linux, mailing lists where developers can interact with one another and develop the newest features for Linux, and newsgroups where anyone can ask questions about and share their enthusiasm for Linux. Following are just a few of these resources.

## Mailing Lists

If you want to hobnob with the Linux development crowd, especially the kernel developers, the place to hang out is on the various mailing lists available to Linux users. Covering topics ranging from hard core kernel development to the promotion of Linux as a business solution, the Linux mailing lists are a subscription service that you can join or leave as the mood strikes you, provided you play by the list owner's rules. Unlike newsgroups and the Web, where everyone is able to participate as they see fit, mailing lists are a little bit more restrictive. This is done so that the signal-to-noise ratio stays high. A list owner or moderator may remove you from a list subscription at their discretion. The following table lists a few of the mailing lists and their submission addresses:

| Mailing List | Submission Address |
|---|---|
| linux-kernel | linux-kernel@vger.rutgers.edu |
| linux-smp | linux-smp@vger.rutgers.edu |
| linux-net | linux-net@vger.rutgers.edu |
| linux-gcc | linux-gcc@vger.rutgers.edu |
| linux-raid | linux-raid@vger.rutgers.edu |
| linux-scsi | linux-scsi@vger.rutgers.edu |

To subscribe to any of these lists, which are managed by Majordomo, send email to <listname>-request@vger.rutgers.edu with subscribe in the message body. For example, to subscribe to the linux-kernel mailing list, you could issue the following command:

```
echo subscribe | mail linux-kernel-request@vger.rutgers.edu
```

In addition to these, and the many other Linux lists managed via the mailing list server at Rutgers, there are mailing lists for most major projects and distributions. Red Hat Linux is no exception. You can subscribe to several lists at Red Hat, including the following:

| Mailing List | Submission Address |
|---|---|
| redhat-announce-list | redhat-announce-list@redhat.com |
| redhat-devel-list | redhat-devel-list@redhat.com |
| redhat-list | redhat-list@redhat.com |

To subscribe to any of the Red Hat lists, the format is slightly different than the ones managed from Rutgers. You must send email to <listname>-request@redhat.com with a subject of 'subscribe' as shown in the following command line, which would subscribe the sender to the redhat-announce-list:

```
mail -s 'subscribe' redhat-announce-list@redhat.com </dev/null
```

## FTP Archives

As your systems grow, you will often find a need to locate software for your Linux system that is not provided on the Red Hat distribution media. This is where the FTP archives come in. Since the early days of Linux, there have been several repositories of Linux software available. Table 2.6 is a list of some of the biggest and most popular software archives for Linux users and a description of the software you will find there.

Table 2.6 Popular Linux FTP Archives

| FTP Site | Description |
|---|---|
| tsx-11.mit.edu | One of the original Linux archive sites located at the Massachusetts Institute of Technology. A good source for new releases of XFree86 for Linux, the GNU C compiler, and many other software packages for a Linux system. |
| metalab.unc.edu | Formerly known as sunsite.unc.edu, this repository at the University of North Carolina is probably the best-known Linux archive in the world. If it is available for Linux, chances are that you can find a copy of it here. |
| ftp.*.kernel.org | A system of mirror sites for Linux kernel sources, you replace the asterisk with a country code, for example us for the United States. |
| ftp.redhat.com | The primary Red Hat FTP site, where you will find the latest official distributions. |
| updates.redhat.com | When updates are posted for the Red Hat distribution, they are uploaded to this site. |
| developer.redhat.com | The Red Hat developer community has a number of trusted developers who upload to this site as part of the Red Hat Contribution Network. |
| contrib.redhat.com | The site where anyone who can make an RPM is allowed to upload a packaged software product. |

## Newsgroups

In addition to the Web and mailing lists, there are a great many Usenet newsgroups devoted to the Linux operating system. Table 2.7 is a partial listing of some of the major newsgroups and their focus.
