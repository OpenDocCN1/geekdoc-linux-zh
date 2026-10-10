your new repository along with the old ones. Several Yum repositories exist, mostly for Red Hat and Fedora, such as the following:

**Livna**  This repository (http://rpm.livna.org/rlowiki/) hosts multimedia tools, such as additional codecs and video drivers.

**KDE Red Hat**  Red Hat and Fedora favor the GNU Network Object Model Environment (GNOME) desktop environment, although they ship with the K Desktop Environment (KDE). The repository at http://kde-redhat.sourceforge.net provides improved KDE RPMs for those who favor KDE.

**Fresh RPMs**  This repository (http://freshrpms.net/) provides additional RPMs, mostly focusing on multimedia applications and drivers.

Many additional repositories exist. Try a Web search on terms such as *yum repository*, or check any Web site that hosts unusual software you want to run to see whether it provides a Yum repository. If so, it should provide an RPM or other instructions on adding its site to your Yum repository list.

> The RPMFind Web site, http://rpmfind.net/, is an extremely useful resource when you want to find an RPM of a specific program, but it’s not accessible as a Yum repository. RPMFind includes links to RPMs built by programs’ authors, specific distributions’ RPMs, and those built by third parties.

# Handling Debian Packages

In their overall features, Debian packages are similar to RPMs, but the details of operation for each differ, and Debian packages are used on different distributions than are RPMs. Because each system uses its own database format, RPMs and Debian packages aren’t interchangeable without converting formats.

# Debian Package Conventions

As the name implies, Debian packages originated with the Debian distribution. Since that time, the format has been adopted by several other distributions, including Ubuntu and Xandros. Such distributions are derived from the original Debian, which means that packages from the original Debian are likely to work well on other Debian-based systems. Although Debian doesn’t emphasize flashy GUI installation or configuration tools, its derivatives add GUI configuration tools to the base Debian system, which makes these distributions more appealing to Linux novices. The original Debian favors a system that’s bug-free as possible, and it tries to adhere strictly to open source software principles rather than invest effort in GUI configuration tools.

Like RPM, the Debian package format is neutral with respect to both OS and CPU type. Debian packages are extremely rare outside Linux, though.