| Action | Description |
| :--- | :--- |
| autoremove | Removes any unneeded packages automatically installed as a dependency of another installed package |
| full-upgrade | Works the same as upgrade but will remove any installed packages required to upgrade the entire system |
| install | Installs a new software package from the repository |
| list | Displays the currently installed packages |
| purge | Removes the specified application, along with any configuration or data files |
| reinstall | Attempts to reinstall an existing package from the repository |
| remove | Removes the specified application, but keeps any configuration or data files |
| satisfy | Attempts to resolve software dependencies in the installed packages |
| search | Searches for a specific package in the repository |
| show | Displays information about the specified package |
| update | Downloads package information from all configured repositories |
| upgrade | Installs available upgrades from all installed packages |

Installing a new package from the repository is as simple as specifying the package name with the install action:

```
```
$ sudo apt install zsh
Reading package lists... Done
Building dependency tree
Reading state information... Done
Suggested packages:
  zsh-doc
The following NEW packages will be installed:
  zsh
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 767 kB of archives.
After this operation, 2,390 kB of additional disk space will be used.
```
```