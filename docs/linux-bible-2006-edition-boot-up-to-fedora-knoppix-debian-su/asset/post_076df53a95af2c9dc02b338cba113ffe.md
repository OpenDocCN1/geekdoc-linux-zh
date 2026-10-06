
# Chapter 12 ♦ Running Yellow Dog Linux 379

| Option | Description |
|---|---|
| yum update | Updates all packages on the system. (Same as preceding option but does not specify package name.) |
| yum remove package | Removes the package identified in package. |
| yum info package | Provides detailed information on the package identified in package. |

Using this information, assume that you want to run gimp—GNU Image Manipulation Project (GIMP) is a very popular graphics editing program—and you haven't installed it previously. If you want to get more information on it, run:

- yum info gimp

If you decide to install it:

- yum install gimp

If an update becomes available a week later and you want to patch it:

- yum update gimp

If it has been a month and you decide no longer need gimp, you can remove it with the following:

- yum remove gimp

Yum makes updating packages very easy and should be used regularly to keep your system updated with the latest patches (you can even run it from a cron job for true automation).

# Running Mac Applications with Mac-Linux

Mac-Linux is a very interesting project that enables Mac users to have the best of both Linux and Mac. With this software, you can run Linux as the primary operating system and still access your Mac OS or OS X operating systems (even another Linux operating system) a window within your operating Linux session.

Mac-linux presents a virtual machine that provides a real environment to the Mac OS or OS X installation. Because there is no emulation, Mac-Linux is very fast and capable. Mac-Linux is very stable and works with minimal configuration. For more information on what Mac-Linux provides and on instructions for its use, visit http://maclinux.org/.

# Support Options

If you run into problems using or installing Yellow Dog Linux, you can obtain support in many ways. The Linux community is very supportive, proffering numerous pages to assist the newcomer. If you encounter problems with hardware, try one of the following options:

- Dog Mailing List Archive Search — A free service that enables you to search some of the more common problems encountered by users. Use the Search Lists box at the top-right side of the http://yellowdoglinux.com/support/installation/ page.
- Yellow Dog Community Board — Another free support option that is run by Yellow Dog Linux enthusiasts. It is available at http://yellowdog-board.com/.
- Yellow Dog Mail Lists — If you don't get answered through the preceding sites, you can subscribe to some of the numerous Yellow Dog mailing lists where you can ask your questions. For directions use at http://lists.terrasoftsolutions.com/mailmanlistinfo.
- Yellow Dog User Channel — If you are comfortable with IRC (Internet Relay Chat), you can use irc.reenode.net and join #yellowdog interaction
- Yellow Dog Official Support — If you can’t find the information you need from the previous sources or http://yellowdoglinux.com/installation/, you can purchase support from Terra Soft Solutions through http://terrasoftsolutions.com/tss_contact.shtml. If you purchased Yellow Dog Linux through Terra Soft Solutions with 60 days of support, you can contact the company through http://terrasoftsolutions.com/

If you need support after your installation, use some of the other generic support options available from the Linux community. These options include using a search engine to find the problem and visiting community-driven sites as the following:

- The Linux Documentation Project (http://tldp.org/) — The Premier site for how-guides to using the Linux operating system.
- Linux Journal Help Desk (http://linuxjournal.com/helpdesk.php) — Offers guidance on Linux.
- Just Linux (http://justlinux.com/) — Offers some basic guides on Linux use.
- Linux.com Tips (http://tips.linux.com/) — Offers great tips.

You can use your search engine to find more of the many, many helpful Web sites out there.

# Chapter 12 ♦ Running Yellow Dog Linux 381

The Linux community is generally very supportive of new users, and you can find help from local Linux User Groups (LUGs) or via many places on the Internet.

# Summary

Yellow Dog Linux is a very stable, fully functioning version of Fedora Core available on the PowerPC platform. It has the capability to extend the life of your Mac hardware and to run Mac OS 9 or below or even Mac OS X on your Linux installation using Mac-on-Linux. Linux is not the sole domain of the X86 community, and now PowerPC users can use Linux while still enjoying their Mac OS or Mac X environment through multibooting or using the innovative Mac-on-Linux software.

As Apple plans to move its product lines from PowerPC to x86 architecture, look for the sponsor of Yellow Dog Linux, Terra Soft Solutions, to set its own course for porting Linux distributions that run on Power hardware. Already, Terra Soft Solutions has begun delivering high-performance rackmounted computers based on Power architecture, along with workstations that focus on strong multimedia support for traditional Mac users looking to switch to Linux.

# Running Gentoo Linux

# CHAPTER

# In This Chapter

Gentoo is a rising star of Linux distributions among enthusiasts. Of all the popular distributions, this is the first one I would recommend to a technically oriented friend who wanted to learn Linux, and the last one I would recommend to my wife ("Just show me what button to click for my e-mail"). That's because to install and maintain Gentoo effectively, you have to care (to an almost unnatural extent) about what is going on with your computer.

- Understanding Gentoo
- What's in Gentoo
- Installing Gentoo

This chapter describes why you might want to use Gentoo, what the Gentoo community is like, and how to get to Gentoo Linux.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_414_0.png)

The Gentoo minimal install CD image is included on the CD that comes with this book. You can copy and burn the Gentoo image to a CD as described in Appendix A. Because you have a minimal install image, you will need some medium containing the needed Gentoo packages (CD, DVD, or hard disk) to get the software you need to complete the Gentoo installation.

# Understanding Gentoo

Performance and efficiency were the critical goals that led to the creation of the Gentoo Linux distribution. A dedication to the spirit of open source software (and to those drawn to it) has been vital to Gentoo's rapid and incredible growth.

In the years it has been in existence, Gentoo has grown from having one maintain—its creator, Daniel Robbins—to having more 250 active developers. It boasts perhaps the strongest community among all Linux distributions. Gentoo users seem willing to contribute so freely because they feel they get back what they give.

# Choosing and Installing a Linux Distribution

The Portage software management system is the key technology that separates Gentoo from other Linux distributions. Based on the Ports system, Portage can be used to build almost the Gentoo distribution from source code, and manage and upgrade that software as well.

# Gentoo's Open Source Spirit

Although Gentoo could produce a Linux distribution, Robbins and the Gentoo project are committed to the goals of open source software, while still allowing those who use the software to make money. Ways that those goals are realized in Gentoo—and not in other distributions—include:

- Passing bugs upstream — Software bugs in open source projects are often shaken when actual Linux distributions are put together. When distribution finds a bug, it is considered good practice to pass the fix to that bug upstream, to the project maintaining the original software. Not passing bugs upstream could potentially gain a commercial distribution advantage over other distributions that do not have the fix. There have been many cases where fixes are in early Red Hat Linux and other commercial distributions have not made to the upstream projects. Gentoo, on the other hand, has a reputation for sharing bug fixes with the open source community.

- Transparent development process — Not only is the open source software available to everyone, but the tools for building that software are also freely distributed. Gentoo users can see exactly what their software contains, along with all the decisions made to build that software. It is also a fairly procedure for users in the process of building their own Gentoo software to change any of those defaults.

- Choices for creating Gentoo — You can build any Gentoo Linux from the source code (as described in this chapter) or start from prebuilt binary packages provided by the Gentoo project. Freedom, in the Gentoo philosophy, means to let users choose the kind of Linux system the users want. So, if users want to make decisions about how the packages are built, they can simply use ready-made packages from the Gentoo project.

- Not-for-profit organization — When the Linux distribution is dedicated to the community and not behold to stockholders, open source enthusiasts often feel better about freely contributing to improving that distribution. Gentoo is a not-for-profit organization.

This open source spirit has also helped Gentoo gain a community that is extraordinarily active and helpful to one another.
