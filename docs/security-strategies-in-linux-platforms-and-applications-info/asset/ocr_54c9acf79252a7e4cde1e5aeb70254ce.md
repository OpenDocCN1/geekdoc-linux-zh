# CHAPTER 2 | Basic Components of Linux Security

# A Basic Comparison: Red Hat and Ubuntu

This book focuses on two Linux distributions: Red Hat Enterprise Linux and Ubuntu Server Edition. The developers behind these distributions have made different choices. Although the Red Hat and Ubuntu distributions occupy a large share of the Linux marketplace, there may be another distribution that better fits your needs. Understanding the differences between these distributions can help you make a better choice.

The biggest difference may be the package-management system. Not surprisingly, Red Hat uses the Red Hat Package Manager to build packages from source code and install them on the Red Hat Distribution. Because Ubuntu its distribution from Debian Linux, it uses the Debian Package Manager to build and install its packages.

There are also similarities between these distributions. For example, Red Hat and Canonical (Ubuntu) both release distributions with long-term support. Red Hat supports its Enterprise releases for seven years. Ubuntu has declared that it would release its Linux distribution every 18 to 24 months, it has been more than three years since the release of Red Hat Enterprise Linux 5. Because of the delay, Red Hat has extended support for this release seven years.

Ubuntu releases every six months, and releases more robust every two years. These releases are noted as long-term support (LTS) releases. The server edition of Ubuntu LTS is supported for five years.

Along with long-term support, Red Hat and Canonical have made a number of other similar decisions. Both companies offer subscriptions to a Web-based support tool that allows authorized users to administer groups of Linux systems remotely.

Both Red Hat and Canonical have made similar choices for default services. For example, both use Apache as the default Web server, the very secure File Transfer daemon (vsftpd) as the default FTP server, and the Common UNIX Printing System (CUPS) as the default printer. The GNU Network Object Model Environment (GNOME) as the default graphical desktop.

There are differences that go beyond the package-management system, however. For example, Ubuntu includes a minimal installation option with its server release, well suited for bastions on virtual machines. That installation includes a kernel optimized to work as part of a virtual guest.

Red Hat and Ubuntu have also made different choices in terms of default applications. In many cases, Red Hat and Ubuntu also these alternatives.

Sometimes, Red Hat and Ubuntu learn from each other. Given their releases under open source licenses, they can take the source code from a competitive distribution and use it themselves. Ubuntu uses a GUI administrative tools originally built for Red Hat. Red Hat is in transition from Xen to the Kernel-based Virtual Machine (KVM) as its native virtualization platform, already in use by Ubuntu systems.

![](bbox=[0.915, 0.203, 0.985, 0.335])