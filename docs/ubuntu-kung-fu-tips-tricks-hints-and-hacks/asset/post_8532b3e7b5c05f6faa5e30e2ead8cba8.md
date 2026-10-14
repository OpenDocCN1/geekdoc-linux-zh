
# Table 6-2. Typical software administration commands (apt top, dpkg bottom).

| Command | Details |
|---|---|
| `apt-get update` | Update the list of available software from the repositories (equivalent to Synaptic’s RELOAD button, and, as such, should be used before any software installation). |
| `apt-cache search searchterm` | Search the repositories for *searchterm*. The specific name of matching packages along with summary descriptions will be returned. |
| `apt-cache show packagename` | Show details of *packagename*, including what dependencies it has, and its full description. |
| `apt-get install packagename` | Install *packagename*. Any dependencies will be automatically added to the list, and you’ll be asked to confirm the total install tally. Multiple packages can be specified. |
| `apt-get autoremove packagename` | Uninstall *packagename*, along with any *unused* dependencies. To uninstall only the specified package, and leave dependencies in place, use `apt-get remove packagename`. If issued without specifying a package, `apt-get autoremove` will attempt to remove all redundant dependency packages on the system. |
| `apt-get upgrade` | Update to the latest versions of installed software. |
| `apt-get dist-upgrade` | Effectively, this command upgrades the entire system to the newest release of Ubuntu. |
| `apt-get clean` | Clears the package cache; useful if disk space is tight, but otherwise not necessary. |
| `dpkg -i packagename.deb` | Manually install the file *packagename.deb*, assuming you have manually downloaded it. |
| `dpkg -r packagename` | Uninstall *packagename*; it is necessary to specify the package name as it’s known on the system (i.e. within Synaptic), rather than the package filename, as required for installation. |
| `dpkg -P packagename` | Uninstall *packagename*, also removing its configuration files. |
| `dpkg -I packagename.deb` | Show information about *packagename.deb*, including full description and dependencies. |
| `dpkg -l packagename` | List details of installed package called *packagename*, including version number. |

> NOTE Bear in mind that dependencies typically have their own dependencies! In other words, it's likely that you'll source all the dependencies needed by the program, only to be presented with an entirely new list! This situation is known as "dependency hell", and is the main reason why APT was invented.

Packages that have been manually installed can be removed using Synaptic, just like any other software.

# Command-line software management

As useful as it is, Synaptic is little more than a graphical front-end for a series of commands that administer the APT software subsystem.

The two most useful commands are apt-get and apt-cache. In addition to these commands, it is possible to install packages you've manually downloaded using the dpkg command.

Installing software at the command-line can be quicker and more efficient than using Synaptic, so is a skill worth learning.

> NOTE Of course, command-line software installation is also possible if the GUI isn't working. It can therefore be very useful when trying to repair a broken system.

In the sections below, I look at the same common software installation tasks mentioned previously, but this time at the command-line.

For those who want a quick start, the most useful subset of software administration commands are outlined in Table 6-2. Remember that software installation requires root powers, so each software install or remove command should be preceded with sudo (commands that search or display information do not usually require root powers).

> TIP Some people prefer to use the aptitude command instead of the APT commands. aptitude is slightly better in how it handles dependencies, and features a semi-GUI interface that makes it easy to use. For more details, see http://algebraicthunk.net/~dbrowne/projects/aptitude/doc/en/.

# Installing software

Here are the steps required to install the Frozen-Bubble game, as discussed previously.

1. The first command to type before installing any software is sudo apt-get update. This will grab the latest list of software from the repositories.
