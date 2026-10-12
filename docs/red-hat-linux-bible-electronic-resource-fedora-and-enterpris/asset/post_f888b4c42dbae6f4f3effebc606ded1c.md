
updates. As with `rhn_register`, you need root access to your computer to run `up2date`. This is because `up2date` needs permission to change configuration files and install packages.

The `up2date` configuration file (`/etc/sysconfig/rhn/up2date`) determines the behavior of `up2date`. Here are a few of the key settings in the `up2date` configuration file to help you understand what `up2date` will do when you launch it:

- Debugging is disabled by default. Change `debug=0` to `debug=1` to turn on debugging if you are having trouble with `up2date`.
- Downloaded packages are stored in the `/var/spool/up2date` directory. Once they are installed, the packages are deleted (by default).
- The `up2date` log file is `/var/log/up2date`. You can open the file in any text editor to see descriptions of everything `up2date` did.
- Any packages that begin with the word `kernel` are skipped. Add other package names you want skipped to the `pkgSkipList=kernel*` entry. You can use shell wildcard characters, such as the asterisk shown in the example, to match all kernel packages.

The `up2date` configuration file contains other settings that you can use to further refine your `up2date` session. For example, you can identify an HTTP proxy server, change the number of failed network-connection attempts that must occur before an exit, or indicate that you want to retrieve source packages along with the binary packages.

The `up2date` sources file (`/etc/sysconfig/rhn/sources`) is another configuration file you might consider making enhancements to. In particular, if you want to get updates of packages already installed on your system from yum or apt repositories, you can add the locations of those repositories to this file. The following two lines contain examples of entries you could add to the sources file for yum and apt repositories, respectively:

```
yum fedora-9-i386-stable http://download.fedora.us/fedora/redhat/9.0.93/i386/yum/stable
apt freshrpms-9-i386 http://ayo.freshrpms.net redhat/9/i386/ updates freshrpms
```

The yum example shows the service as `yum` and the channel name is `fedora-9-i386-stable`, followed by the location of the yum repository. In the apt example, the repository is divided into three parts: the host name, path, and final directory. Notice that in this example, both `updates` and `freshrpms` directories are available repositories. Once you have added a line similar to the ones just shown, they appear as channels in the Channel window when you run `up2date`.

To use the official locations for packages from Red Hat Inc., you can simply use the default `up2date` settings. Here’s an example of an `up2date` session:

- 1. Type **up2date** or click the notification icon and select Launch `up2date`. If your system does not yet have the Red Hat public key, you will be asked if you want to have `up2date` install it. (The key is needed to verify that the packages you are receiving are signed by Red Hat.)
- 2. Click Yes to install the key. The Red Hat Update Agent window appears.
- 3. Click Forward. The Channels window appears.
- 4. The Channel indicates the version of Red Hat Linux you are running. Select the Channel appropriate to your Red Hat installation and click Forward. The Update Agent begins checking your available packages.
- 5. The Available Package Updates window appears, displaying packages available for updates. Click each package you want to update or click Select All Packages to have all applicable packages updated. You can click on a package and then click View Advisory to see which advisories are addressed by updates for the package.
- 6. Click Forward to continue. The Update Agent begins testing packages to check for dependencies among the packages you are updating. If any dependencies arise from the packages you selected, the Packages Required to Solve Dependencies window appears, listing the additional packages you need.
- 7. Click Forward to have the packages shown included in the updates (or click the back button to change your package list). The Retrieving Packages window appears and notes the progress as the packages are downloaded from the Red Hat Network.
- 8. Click Forward to begin downloading the packages to your computer. (This may take a while, depending on the speed of your Internet connection and the number of packages you are downloading.)
- 9. When all packages are downloaded, click Forward. The Installing Packages window appears.
- 10. Click Forward to begin installing the packages you have downloaded.
- 11. When all the packages are installed, click Next. The All Finished window appears, displaying the package name and version for each package that was installed.
- 12. Click Finish to end the session.

If you are interested in seeing how the upgrades went, you can do the following:

- Check the log file (/var/log/up2date).
- See if any packages were left behind in the spool directory (/var/spool/up2date).

Though you don't necessarily have to reboot Linux at this point, if new daemon processes are installed with any of the updated packages you might want to restart them. For example, to restart your Web server (httpd daemon), you could type the following as root user:

```
# /etc/init.d/httpd restart
```

## Using the Red Hat Network

Once you have an account with Red Hat Network you can log in to the RHN site and take advantage of the services it offers. As noted earlier, each registered user is entitled to register one computer to receive automatic updates. Other services that you receive simply by registering with the Red Hat Network Web site include:

- The ability to view complete listings of available errata, including security, bug fixes, and enhancement alerts. Errata are organized by Red Hat Linux version, to take the guesswork out of figuring out compatibility issues.
- E-mail alerts of errata and notification of new packages available to fix the problem.
- An entitlement manager that shows you which systems you are entitled to manage through RHN and lets you add more systems.
- A feature for scheduling actions, such as automatic package update at a specified time.

Go to the Red Hat Network site (rhn.redhat.com) and log in using the user name and account you created during the rhn_register session described earlier. Traverse the RHN site using links on this page. Available sections include:

- **Your RHN** — Contains notifications of the systems that may contain outdated packages. Sections in Your RHN include: Your Account (which contains personal information, such as name, address, e-mail, and so on) and Your Preferences (where you can specify whether or not you want to receive e-mail errata).
- **Systems** — Lets you view a System List, which contains all the systems you have registered with RHN, or use a search tool to search your list of systems.
- **Errata** — From the Errata page you can display all errata, show only those that apply to your system, or do keyword searches of available errata.
- **Software** — A channel designates a version of Red Hat Linux that has package updates associated with it. By selecting the Channel List in this section, you can see what package versions are available for the Red Hat Linux version you are using.
- **Schedule** — You can schedule package installations to occur at a later time. From this page you can also see pending, completed, and archived actions.
- **Help** — For more help with Red Hat Network, the Help Desk offers the RHN FAQ, a customer-service support link, support forums, and the RHN Reference Guide.

If you want to purchase additional entitlements, I recommend that you check the Red Hat Network site for the latest prices. At the time of this writing, $60 per year Basic Service Entitlement is available for Fedora Core. This entitlement lets you get updated packages, but does not offer any technical support from Red Hat, Inc. (Previously, with Red Hat Linux, you could also get limited installation support, but that's not available with Fedora.) For official support, Red Hat is encouraging customers to upgrade to Red Hat Enterprise Linux and purchase the $96 per year Enterprise Service Entitlement.

Without purchasing additional entitlements, you can register additional systems with RHN. However, you can’t use the update mechanism to update those additional systems. To register additional systems, simply run the rhn_register command from each system you
