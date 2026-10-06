
# Chapter 8 ✦ Running Fedora Core and Red Hat Enterprise Linux 279

The highly touted hardware detection done by the KNOPPIX bootable Linux distribution is based on the kudzu libraries from Red Hat, Inc. While the kudzu hardware detection is quite good in Fedora Core and RHEL, if you don't need hardware detection from kudzu, you can save significant time in rebooting if you disable kudzu.

## Red Hat Desktop Look-and-Feel

To add a level of consistency to the desktops on its Linux systems, Red Hat created a look-and-feel that is pretty much the same for GNOME and KDE. Of course there are some differences in color and logos, but a user can expect to find menus, panels, workspaces, and other desktop features in Fedora Core and RHEL systems to be similar.

## System Configuration Tools

Red Hat created a set of simplified, graphical tools for configuring and administering basic administrative features in Red Hat systems. Using these tools, you can add printers, configure your network, add users, set up your sound card, and tune up your video card, to name a few of the features they cover.

Red Hat's graphical configuration tools (which are described in Chapter 4) can be launched from the System Tools or Settings menu or from the command line. Recently, the beginnings of these configuration tools' command names changed from redhat-config to system-config. For example, the tool to configure your network in Fedora is now called system-config-network (instead of redhat-config-network).

## Going Forward with Fedora Core

With the original Red Hat Linux, you could have the exact Linux system for free (to run in your home or small business) that was being used in large-scale enterprise deployments. For just a few dollars, you could add Red Hat support for that system, which included official security patches and upgrade paths for the future.

Today, with the different free (Fedora Core) and subscription-based (RHEL) Linuxes from Red Hat, the same basic advantages hold true—if you are more adventurous. Because Red Hat Linux is such a successful operating system, many who developed skills in using and deploying Red Hat Linux have rallied to support Fedora in areas where Red Hat, Inc. has bowed out. The following sections explore some of those support efforts.

## Growing Community Support for Fedora

Despite some confusion about the future and direction of the Project, new initiatives and Web sites have popped up to support Fedora. One of the best new official assets of the Fedora Project is the FedoraForum.org (http://fedoraforum.org/)'s site recognition as the official end-user choice.

FedoraForum.org features news, galleries, and (as you might guess) forums for sharing questions and information about Fedora. As of this writing, there were over 500,000 posts to these forums and nearly 50,000 members. The forum for posting HOWTO articles has more than 5,000 posts itself.

The Unofficial FAQ (www.fedorafaq.org) has become an excellent resource for getting answers to the most constant, nagging questions about Fedora. This FAQ is a good start for learning how to get all things you need (MP3 players, instant messaging, video players, access to your Windows XP file system, and so on).

On the whole, the total amount of software available and greater stability among software repositories (I discuss next) has made it possible to get a much better experience with Fedora Core than even possible with Red Hat Linux. The strange thing is, that for reasons I describe later, people seem to trust Fedora less than they did Red Linux.

## Fedora Extras

One concern with Fedora Core is as Red Hat adds more enterprise-class features to test using RHEL, more features for home, small office, and educational users will be pushed out. With Red Hat's current momentum to keep Fedora Core to the size of four CDs, packages that have been cut from Fedora are finding their way into Fedora Extras.

Unlike Legacy projects, which consist of updates to software already in the Fedora distribution, the Fedora Extras Project encourages people to build their software into RPM packages that can be easily installed in Fedora Core and Red Hat Linux systems. Guidelines for becoming a Fedora developer are available from the Fedora Extras wiki (http://fedoraproject.org/wiki/extras).

When someone builds an RPM and submits it to Fedora Extras, it is reviewed and, added to the Fedora Extras repository. This process offers several advantages to the Fedora community:

- Packages that people relied on in previous Fedora releases don't just disappear.
- Fedora Extras packages are not necessarily tested as thoroughly as those in Fedora Core, being in Extras adds a level of security and stability to a package that can't be guaranteed if you grab software randomly from the Internet.

The Fedora Extras repositories are automatically added to your yum and update facilities. So, for example, if you know that you want to install the abiword package, you can do so by simply typing yum install abiword as root user. Yum grabs it and installs it from a Fedora Extras repository.

Packages in Fedora Extras are still expected to meet Red Hat's stringent guidelines. This means that you won't find proprietary software drivers (as those used with NVIDIA video cards or wireless cords intended for Windows systems) or with questionable patent issues (such as MP3 or video players).

Another effect of the Fedora Core/Fedora Extras approach, however, is that third-party, RPM-based software repositories have a wider base of common software libraries and utilities to rely upon. The rpm.livna.org repository (which includes many useful software packages that Red Hat will not distribute), depends on the Fedora Core and Fedora Extras repositories.

## Fedora Legacy Project

In April 2004, Red Hat announced that it would end support for Fedora 1 and 2. The Fedora Legacy Project was created to provide updates for these versions for those who could not upgrade immediately. The project also encouraged users to move to Fedora 3 or 4, which contained the latest features.

In April 2005, Red Hat announced that it would end support for Fedora 3 and 4. The Fedora Legacy Project was expanded to include these versions as well. The project continued to provide security updates and encouraged users to move to Fedora 5 or 6, which contained the latest features.

In April 2006, Red Hat announced that it would end support for Fedora 5 and 6. The Fedora Legacy Project was expanded to include these versions as well. The project continued to provide security updates and encouraged users to move to Fedora 7 or 8, which contained the latest features. (Note: reconstructed text context)

# Chapter 8 ✦ Running Fedora Core and Red Hat Enterprise Linux 281

## Forums and Mailing Lists

Since Fedora came into existence, many individuals and organizations have rallied to support Fedora going forward. If you want to get into the flow of the Fedora community, I recommend starting with the Fedora Project's mailing lists. Many other Fedora resources are also available on the Web, and Appendix B includes a list of many of them.

## Listening to the People at Red Hat

Red Hat sets out the charter for the Fedora Project on its home page (http://fedora.redhat.com):

> The Fedora Project is an open source project sponsored by Red Hat and supported by the Fedora community. It is also a proving ground for new technology that eventually makes its way into Red Hat products. It is not a supported product of Red Hat, Inc.

What that means is still being sorted out two years after the launching of the Fedora Project. What it means so far has been four versions of Fedora Core that have brought in development of different technologies than were included in Red Hat Linux.

Red Hat has close to its plan to release Fedora two to three times per year. So releases have stayed closer to the two-year pace average was the standard for producing Red Hat Linux, although plans for the soon-to-released Fedora Core is expected to land closer to an eight-month development cycle. Red Hat will also stick to its promise to include Fedora technology in its commercial products.

Each release of our supported products will be based in a recent release of Fedora Core. Software in Red Hat Enterprise Linux 3 matched almost exactly the same packages that were in Fedora Core 1. Likewise, the same was true with Fedora Core 3 when Red Hat completed Red Hat Enterprise Linux 4. As for including the Fedora community in Fedora development, Red Hat states on the Fedora home page:

Red Hat will retain editorial control over The Fedora Project but will explicitly include external developers in the process of making technical decisions that
