Two options require a little more explanation. The reload option does not stop or start a service. It just reloads the configuration file. If you've just changed a configuration file, it's a quick way to put it into effect without restarting a service. A restart would kick off any connected users.

The constrestart restarts a system only if the system was already running. /etc/init.d/ scripts include a number of other options; perhaps the most important include the word force in the script, which can be helpful if a service is not responding to commands.

While developers are working on replacing regular service scripts in the Upstart system, it is unlikely that the /etc/init.d directory will be completely replaced in stable Linux distributions. And if they are, developers will have to make the change appear seamless to the administrator.

# Isolate with chroot Jails

Conceptually, a chroot jail is sort of a virtual machine. In fact, it's considered by some as type of operating system-level virtualization. In most cases, a chroot jail includes all of the binaries, libraries, configuration files, and executables required to run a service that is contained. A properly configured chroot jail does not allow privilege escalation of any sort, whether without SUID or SGID-bit modified executable files or other means of gaining administrative access.

If a black- hacker is able to break into a service, his actions should be confined to the files and subdirectories in the chroot jail. With administrative access, hacker may be able to break out of chroot jail into the main directory tree for the local system.

Significant services that have been configured with chroot jails include the Berkeley Internet Name Daemon (BIND) software for DNS, the very FTP daemon (vsFTPD), and the Postfix email server. As described in Chapter 5, the vsFTPTP chroot jail would be configured to limit both anonymous and regular users to appropriate directories.

One interesting implementation of a chroot jail is based on the Red Hat bind-chroot package, which configures the files needed for the BIND DNS service in the /var/named/chroot/ directory. For more information on BIND and Postfix, see Chapter 9.

# Avoid X Servers and X Clients Where Possible

Regular users demand the GUI. So it's impossible to avoid the GUI in most situations. But the GUI isn't required for most systems with Linux servers. It isn't even required for servers that share graphical images such as the Apache web server. Since the GUI presents a number of security risks, you should avoid installing the GUI on Linux servers when possible.

In Linux, X is a common reference to the GUI. The main server for Linux is based on the work of developers sponsored by the X.org foundation. The X server uses hardware on the local system to display graphical images. These images come from X clients, which may be either locally or remotely.