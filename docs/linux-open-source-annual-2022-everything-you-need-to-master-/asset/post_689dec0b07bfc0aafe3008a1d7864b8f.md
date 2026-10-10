
# Arch-based distros
**The Verdict**

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_22_0.png)

For some users, having a purely GTK or Qt system will be a boon, even if it drastically restricts the number of applications that are available to them. For those people Antergos, and in particular KaOS, may have some appeal. Others will be happy that cross-toolkit theming is in much better standing than it once was and not mind installing both toolkits. Storage is cheap, after all.

In many ways we felt that KaOS should be offering newer KDE packages, being as it does hit the Arch repos soon after release. Of course, KDE neon is considered the premier distro for showing off the latest and greatest on planet Plasma, so maybe there’s no point competing with that. The Blue Systems sponsored Netrunner Rolling is a fine effort, but we felt it was trying to cover all bases.

Fantastic efforts of each distro notwithstanding, users who are unfamiliar with Arch and its ways of working will sooner or later find themselves confused. Manjaro may be the most user-friendly of this month’s picks, but Ubuntu or Mint it is not, and treating it thusly will lead to disappointment. (Life is full of disappointments, but that’s a story for another Roundup.) You’ll probably have to get your hands dirty at some point. Conversely, if you’re familiar with Arch then you may very well prefer to stay there (up on that high horse you mean? – Ed), or perhaps take inspiration from these distros and apply it to your Arch install. We were certainly enamored by ArchLabs’ desktop zen, and what can be done with a less than 200MB memory footprint.

Manjaro does a great job with its flagship Xfce edition. It shows that this desktop is capable of looking good as well as being considerate on resources. It’s become hugely popular over the past year, not so much because of people’s gripe with Ubuntu, but because it’s a darn fine distro that gives people exactly what they want. When Xfce 4.14 is released and journalists become tired of making jokes about that, this will surely become ever the more greater.

The Gnome and KDE flavours are fine too. Great if you prefer the latest desktop fripperies, but we admire Manjaro’s boldness in focusing on Xfce.

**1st Manjaro 9/10**
Web: https://manjaro.org
Licence: Various
Version: 18.10
Manjaro has tamed Arch into something both humans and robots can enjoy.

**2nd ArchLabs 9/10**
Web: https://archlabslinux.com
Licence: Various
You don’t need an ancient machine to enjoy a lightweight distro.

**3rd Antergos 8/10**
Web: https://antergos.com
Licence: Various
Version: 18.11
Fantastic installer and a great all-round distro.

**4th Netrunner Rolling 7/10**
Web: https://netrunner.com
Licence: Various
Version: 2018.08
KDE Plasma and Arch are a winning combination, but still a few rough edges.

**5th KaOS 7/10**
Web: https://kaosx.us
Licence: Various
Version: 2018.10
One for Plasma/Qt purists, but this makes it limiting for everyone else.

## ALSO CONSIDER

Several Arch-based distros have come and gone over the years, but some have stood the test of time and new ones spring up regularly. It’s common for distros to add non-free software to improve the user experience, but Parabola and more recently Hyperbola go to the other extreme. These two, as well as being named after curses, are both FSF-approved and use the Linux-libre kernel. Hyperbola takes inspiration from Debian, using an older, tried ‘n’ tested kernel. Arch may have stopped supporting 32-bit, but the Arch Linux 32 distro is alive and well.

Arch-Xference and Anarchy Linux, both Xfce affairs, are worth a look. Chakra Linux, a KDE offering, impressed us last year, but hasn’t been updated since then. Those wanting something even more lightweight than ArchLabs should check out ArchBang, which was inspired by the now-defunct CrunchBang. In a roundabout way this inspired ArchLabs too.

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_23_0.png)

# USING BSD FOR LINUX USERS

Aaron Peters is a stranger in a strangely familiar land as he dives into installing and using Linux's open-source cousin FreeBSD...

If you're reading this, then you have at least a passing interest in free software. Maybe it's limited to Linux, but the FOSS community is bigger than that. There's plenty of software projects that run on other operating systems, and also a variety of open source Un*x clones.

The BSD family of operating system is an important example, representing some of the first systems truly free from legacy Unix code, and can be seen as at least an uncle to Linux as we know it today. What started as one system, the Berkeley Software Distribution (BSD) went through a variety of versions (a book in itself), with different projects and vendors. Today's family of BSD systems include NetBSD, OpenBSD, and TrueOS. Of these, FreeBSD is considered the most ‘general purpose’ and is arguably the most popular. Notably, Apple used FreeBSD code as the basis for the Darwin project, an OS that became Mac OS X (and now macOS).

If you're looking for a desktop system to install and immediately be productive with, there's better options for you (see the sidebar for some other members of the BSD clan). But this article intends to be a learning exercise to see how this little Unix-y devil stacks up. And FreeBSD offers that learning opportunity by being more hands-on than other desktop-oriented systems, whether Linux or BSD. However, the author did have a goal – to be able to take this from a fresh install to a ‘productivity system’ complete with a GUI interface and accompanying tools. But along the way, we're aiming to see what's the same, as well as what's different.

And as we in the open source community know, variety is the spice of digital life. So we owe it to ourselves to explore this BSD system and see what's what.

Why use FreeBSD? A better question might be “Why not use FreeBSD?” As we’ll see, FreeBSD comes from the same Unix® roots as Linux, and we can expect our skills to transfer over nicely. Oh, there will be slight differences for sure, but a shell is a shell is a shell, and your ls command in FreeBSD will indeed list the contents of your current directory.

But there’s always something to be learned from different ways of doing things, and some of the areas where FreeBSD excels include:

- As a server. FreeBSD powers some of the most basic services on the internet, and is also used in some of the network hardware that makes up its infrastructure.
- Security. Its beginnings as a server OS have led to FreeBSD including a number of unique security features, such as access control lists (ACL), a choice of powerful firewalls, and jails for running virtualised OSes.
- Following documentation. With many modern Linux distros, getting installed is a simple point-and-click affair. In contrast, FreeBSD comes from an era where you actually had to read the documentation, understand it, and follow along closely.
- A focus on compiling source. The Ports system gives a fantastic introduction to compiling software for those who aren’t software engineers by training.

Use FreeBSD for fun. Use it to learn, and evangelise it to others in the community – we’re family after all. The way you install FreeBSD is just like Linux, in that you need to get some sort of installation medium, then boot your machine from said medium. The main differences during installation are threefold. First, the installer is text-based. Second, the installer doesn’t give the option to move back to previous screens. Finally, the way you include software during the install is rather unique.

In this context, “include” software doesn’t mean actually installing it. But the installer does give you the option to add the FreeBSD Ports Collection. Ports is the equivalent of Linux package repositories, except that they’re used to build packages rather than install.

For now, if you’ve installed a Linux distro, you’ll breeze through the text-based installer’s screens:

- First up, a couple of environment screens: Keymap selection, and choosing a hostname for your machine.
- Select the “distributions”. As mentioned, make sure you include Ports. Think of these as software sets, rather than the colloquialism for a Linux-based OS.
- Disk partitioning. The first option will be between the traditional UFS and the newer ZFS filesystems. For testing, UFS is fine. You’ll be offered the usual manual partition or take over the whole disk. You’ll also have a choice of several different partition schemes.
- The installer will start decompressing the distro onto your drive. Don’t go anywhere, it won’t take long.

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_24_0.png)

Finally, some quick system configuration, including setting up the root user, network, time zone, date/time, services (SSH is selected by default), security options, and user account(s).

There are sub-steps, and it may seem like we glossed over the installation. But honestly, if you’ve done a Linux install you’ll have no troubles. For those of us of a certain age, step 2 might even bring back fond memories of writing sets of Slackware floppy disks.

## Booting into FreeBSD

That Nostalgia will continue once you reboot your system. You’ll get to see the plain-text system messages blur past in all their glory, and when all is said and done you’ll land at a login prompt – no fancy desktop, no new-fangled session manager. You’ll see login: and that’s it. It doesn’t even clear the screen for you.

But start poking around and things will begin to get familiar pretty quickly. Your home directory is in `/home/username/`, and the standard sh shell is similar enough to Bash that you won’t notice the difference.

The first thing that will probably jump out at you is that sudo isn’t installed by default, so you’ll need to use the actual root account to make changes. But otherwise all the basics are there: `cp mv` for shuffling files, `mkdir` for new directories, and `cd` to get yourself around.

That said, your system is definitely barebones. Take a tour around your executable directories (`/bin`, `/sbin`, `/usr/bin`, and `/usr/sbin`) if you don’t believe me. You’ve got basically enough to do some text editing (with either `edit` or `vi`/`nv`). In order to make this a useful system, we’ll need to get started installing some programs.

> Note: one area where the author ran into some delays is in setting up the bootloader. In part, this has to do with his stubborn insistence on trying to make it work with the native Windows boot manager on this dual-boot device.

Things went much more smoothly once FreeBSD was allowed to take over the entire disk, and even just installing the FreeBSD bootloader would

## MEET THE BSD DEVILISH FAMILY

FreeBSD is similar to Linux in that there’s an extended family of other systems. There’s now quite a few different choices in the BSD world. Here are a few of the most popular:

- **FreeBSD** ([www.freebsd.org](www.freebsd.org)) was originally a server OS first (as most Unix-likes were), but now is positioned as the ‘jack-of-all-trades’ system, if you’re willing to put in the work in, as we’ll cover.
- **NetBSD** ([www.netbsd.org](www.netbsd.org)) is another all-purpose OS, with a focus on running as many different devices as possible, meaning you can just as easily find it on a desktop, a server, or replacing Windows CE on an NEC MobilePro 790 circa 2004.
- **OpenBSD** ([www.openbsd.org](www.openbsd.org)) its claim to fame is security, with all packages going through rigorous audits at the source level.
- **TrueOS** ([www.trueos.org](www.trueos.org)), originally called PC-BSD, this is a desktop-friendly remix of FreeBSD, pre-configured with niceties such as a graphical installer and bundles of apps pre-installed.
- **DragonFlyBSD** ([www.dragonflybsd.org](www.dragonflybsd.org)) forked from FreeBSD and provides a carefully tuned system for high-performance applications.
- **GhostBSD** ([www.ghostbsd.org](www.ghostbsd.org)) is technically a grandchild of FreeBSD, as it’s built off of TrueOS. Just as Linux distros stand on the shoulders of giants, this aims to provide a simpler experience than its parent, with a focus on lighter desktops like MATE and Xfce.
