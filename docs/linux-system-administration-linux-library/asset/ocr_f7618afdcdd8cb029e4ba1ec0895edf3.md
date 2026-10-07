8.2. Many of rpm's less-used features are devoted to the creation of RPM packages by software developers.

# Table 8.1 Common rpm Operations

| rpm Operation | Description |
| -i | Installs a package; the system must not contain a package of the same name. |
| -U | Installs a new package or upgrades an existing one. |
| -F or --freshen | Upgrades a package only if an earlier version already exists. |
| -q | Queries a package: Finds if a package is installed, what files it contains, and so on. |
| -V or -y or --verify | Verifies a package: Checks that its files are present and unchanged since installation. |
| -e | Uninstalls a package. |
| -b | Builds a binary package, given source code and configuration files. |
| --rebuild | Builds a binary package, given source RPM file. |
| --rebuilddb | Rebuilds the RPM database, to fix errors. |

# Table 8.2 Common rpm Options

| rpm Option | Used with Operations | Description |
| --root dir | Any | Modifies the Linux system having a root directory located at dir. This option can be used to maintain one Linux installation discrete from another one, say during OS installation or emergency maintenance. |