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