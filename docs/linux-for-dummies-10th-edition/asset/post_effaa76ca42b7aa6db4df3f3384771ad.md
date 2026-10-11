
## Processes

Most of your system activity requires processes. Even when your system appears idle, a dozen or so processes (programs) are running in the background. These commands, shown in Table A-11, enable you to check under the hood to make sure that everything that needs to be running is running and that you’re not overheating or overtaxing resources.

| **Command** | **Purpose** |
| :--- | :--- |
| `crontab` | Sets up commands to run at regular intervals. |
| `kill` | Stops a process by its number. Often used as `kill -9` for a harsh stop for something that won’t die. |
| `killall` | Stops a process by name rather than number. |
| `nice` | Assigns a CPU use priority to a process. |
| `pidof` | Gets a program’s ID number. |
| `ps` | Gets a lot of programs’ ID numbers, usually used as `ps aux`. |
| `pstree` | Shows the relationships between programs. |
| `renice` | Changes a program’s CPU use priority. |
| `top` | Shows resource use over time. |

## Network

These days most Linux systems are on some type of network, even if it’s just your small home network. The graphical Network Manager tool (see Chapter 9) provides one-stop shopping for configuring your network settings. Linux also provides a series of command line commands to help you manage and even fine-tune your network settings. Table A-12 shows some of the more helpful network-related commands you have available.

Table A-12: Network Commands

| **Command** | **Purpose** |
| :--- | :--- |
| `ethtool` | Display Ethernet settings for a network interface. |
| `ifconfig` | Display or set the IP address and netmask for a network interface. |
| `ip` | Display or set the IP address, netmask, and router for a network interface. |
| `iw` | Display or set the wireless settings for a wireless network interface. |
| `iwconfig` | Display or set the SSID, IP address, and netmask for a wireless network interface. |
| `nmc1i` | Open the Network Manager command line interface. |
| `nmtui` | Open the Network Manager menu-based command line tool. |
| `route` | Display or set the default router information. |

## Appendix B: Linux Distributions

### Linux Distributions

The foundation of the Linux world is the Linux core distributions. These distributions usually contain just about every application available for Linux within the distribution release DVDs, or easily available for download. The core distributions are often where new packages are developed, tested, and incorporated into the Linux distribution.

While literally hundreds of Linux distributions are available, many of them are derivatives of one of these core Linux distributions (see Chapter 1). Each subdistribution inherits the features and some of the ideals of the core distribution. Because of that, it helps to take a closer look at just what are the major Linux distributions.

The major players you run into in the core Linux distribution world are:

- Slackware
- Fedora
- Debian
- Gentoo

This chapter provides a little background information on what makes these core distributions different from one another.

![](img/577d3bff979ee86b07f9836e0df274ce_458_0.png)

It's impossible to list and discuss all the distributions. If you're interested in learning about others, go to www.distrowatch.com, a great up-to-date source of information on all Linux distributions!

### Slackware

Founded in 1993 by Patrick Volkerding, it's one of the oldest Linux distributions still in existence. In the early days, you had to download the distribution as a series of floppy disks!

Slackware is often called the "bare bones" core distribution, mainly because of its lack of customized graphical management tools. It's certainly not for the beginner Linux user, but does offer many benefits for the advanced user.

Slackware installs applications directly from `.tar.gz` source files, so you know your application is being custom built as you install it. In a somewhat controversial move, Slackware only supports the KDE and Xfce graphical desktop environments, preferring to leave out the GNOME desktop environment. You can, however, install GNOME as a separate package.

While many of the Linux sub-distributions based on Slackware have faded from existence, you may recognize one in particular — the openSUSE distribution owes its start to Slackware when it started out as the S.u.S.E. package.

### Fedora

The Fedora Linux distribution came about in 2003 as a derivative of the original Red Hat Linux distribution, which started in 1994. The Red Hat company decided to move Red Hat Linux into the commercial world and focus on servers, but created the Fedora Linux distribution as a free development and testing ground for proving Linux applications. Many of the features incorporated in Fedora eventually make their way to the commercial version, now called Red Hat Enterprise Linux.

Since version 30, Fedora has been released in several varieties:

- **Fedora Workstation**: Uses the graphical GNOME 3 desktop environment.
- **Fedora Server**: Doesn't provide a graphical desktop, customized for data center server environments.
- **Fedora CoreOS**: Provides only the core features with no additional applications. Intended for cloud environments.
- **Fedora IoT**: A stripped-down version of Fedora intended for running on devices.
- **Fedora Silverblue**: Created for developers who use container based workflows.

Besides these officially sanctioned versions, Fedora also supports what it calls spin distributions, or just spins. Spins are LiveDVDs created using the Fedora tools. The most common spins are the Desktop spin, which includes GNOME 3, and the Workstation spin, which includes KDE. You can also download Fedora as a cloud image for OpenStack, as a minimal image for containers, or as a custom system builder (CSB) image that allows you to create your own Fedora system by adding packages in an interactive web interface.

lived-creator tool, and can be customized for any environment. This is a great way to create and distribute your own Linux environment!

Fedora uses a special software package format, called **Red Hat Package Management (RPM)**. This is a common package format, and you see lots of Linux applications that provide customized installs in `.rpm` format. The beauty of RPM is that it can automatically place application files and libraries in the correct location on the system, with no manual intervention required. The Red Hat Enterprise Linux system uses these same package files.

Historically, Fedora has defaulted to the GNOME desktop environment (see Chapter 4), but provides an easy way to install KDE Plasma if you prefer.

Distributions based on the Fedora system are:

- **K12LTSP:** A distribution focused on K-12 school environments, incorporates the Linux Terminal Server (LTS) to share server resources on stripped-down client workstations.
- **CentOS:** A distribution created by manually compiling the Red Hat source code files, which are derived from the Fedora packages. Popular in the server environment as a free alternative to Red Hat Enterprise Linux.
- **EnGarde Linux:** Focuses on creating a secure server environment.
- **Network Security Toolkit:** A LiveDVD with security and networking tools for performing security and network diagnostics and monitoring.

### Debian

The Debian Linux distribution started life in 1993, created by Ian Murdock. It’s supported by one of the more organized open source boards in the Linux environment — The Debian Project. The Debian Project is a complete volunteer organization of software developers that guides the distribution and development of Debian Linux. Each year members of the organization vote for the project leader, who guides the development process, but doesn’t have absolute power over the development of the distribution.

The Debian project is best known for its well-organized hierarchical strategy of versions. Three versions of the Debian Linux distribution are available for download at any given time:

- **Stable:** The latest official release, recommended for most Linux environments.
- **Testing:** The version slated to be the next official release. This version mostly works, but may still contain bugs. Recommended for Linux users to download and play with to help find bugs.
- **Unstable:** The development version, where most of the experimenting happens. Recommended only for advanced Linux users, and for environments where system crashes don't matter!

If you're installing Debian Linux for a production system, you'll definitely want to make sure you grab the stable release! If you like playing with cutting-edge tools, try out an unstable version — just watch out for the sharp edges! One complaint, though, about the Debian system is that it takes a long time for distributions to float their way into the stable environment. Debian Linux is known for having long release schedules!

With three distribution levels to support, you can imagine the work it takes to coordinate things! Debian uses three separate software repositories — one for each distribution level — to support adding software and fixes.

Besides the three main distribution repositories, the Debian project also supports three additional software repositories:

- **Experimental:** A place to grab standard software applications that haven't been customized to run in a Debian environment yet.
- **Volatile Project:** Software applications that are under development of themselves. If the name doesn't say it all, don't ask!
- **Oldstable:** The repository for the previous stable release of Debian.

As you can probably guess, this can make software installation confusing for the beginner, but provides the advanced Linux user a smorgasbord of software choices!

The Debian distribution uses its own package management system (called **dpkg**), which creates `.deb` package files. It also uses the `apt` tool to search repositories for security updates and bug fixes for installed software.
