# APT: the Advanced Package Tool

separation of control is interesting from an administrative standpoint, but it doesn't affect the package distribution systems, except that they may need to be manually added by the administrator.

# RHN: the Red Hat Network

With Red Hat having gracefully departed from the consumer Linux business, the Red Hat Network has become the system management platform for Red Hat Enterprise Linux. You purchase the right to access the Red Hat Network by subscribing. You can use the Red Hat Network as a glorified web portal and mailing list. At its simplest, the Red Hat Network is not much different from the patch notification mailing lists that have been run by UNIX vendors for years. But more features are available if you're willing to pay for them. Current pricing and features, see rhnredhat.com.

The Red Hat Network provides a web-based interface for downloading new packages as well as a command-line alternative. Starting with Red Hat Enterprise 5, the CLI tool is yum; before it was the unwise, dependency-headache-inducing tool update. yum lets you download and install new packages without human intervention. Once you register, your machines get all the patches and bug fixes that they need without you ever to intervene.

The downside of automatic registration is that Red Hat decides what updates you run. You might consider how much you really trust Red Hat (and the software maintainers whose products they package) not to screw things up. Some of the choices Red Hat has made when it comes to time which compiler to ship, some folks might remain skeptical.

A reasonable compromise might be to sign up one machine in your organization for automatic updates. You can take snapshots from that at periodic intervals to test as possible candidates for internal releases.

# APT: the Advanced Package Tool

APT is one of the most mature package management systems. It's possible to upgrade an entire system using software with the apt-get command or even (with the Red Hat Network) to have your boxes continuously keep up to date without human intervention.

The first rule of using apt-get on Ubuntu systems (and all management of Debian packages) is to ignore the existence of dselect, which acts as a front end for the Debian package system. It's not a bad idea, but the user interface is poor and can be intimidating to the novice user. Some documentation will try to steer you towards dselect, stay strong and stick with APT.

If you are using apt-get to manage a Ubuntu installation from a mirror, the easiest way to see the available packages is to visit the master list at packages.ubuntu.com. The web site includes a search interface. If you set up your apt-get server (see page 390), you will know what packages you have made available and you can list them in whatever way you want.

![](bbox=[0.933, 0.613, 0.996, 0.733])