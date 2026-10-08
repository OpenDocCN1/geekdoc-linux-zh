# FILE MANAGEMENT 267

rudimentary example can be found in Listing 10.4. As a rule, however, use of a complete backup system is the better choice (see also Chapter 7).

```
(Linux):$ find -print|afio -ozf /dev/fd0
./.profile
./.emacs
./.diary
..
(Linux):$ touch .backup
(Linux):$ find -newer .backup -print|afio -ozf /dev/fd0
./.bash_history
```

**Listing 10.4** Data backup with find and cp.

After the installation of a LINUX distribution, several files must be adjusted manually, for example the /etc/printcap file. One after the other, more modifications are carried out to adapt the system to the specific requirements. This is either done manually or using the distribution tools. For a backup, to find out which files have been modified, one could create the file Install_Date in /root directly after the installation of a LINUX system (Listing 10.5).

```
(Linux):# root date > /root/Install_Date
```

**Listing 10.5** Creating a file that contains the installation date.

It is not necessary to save the date in a file; however, if the modification date of a file was inadvertently changed, for example with touch, it is always possible to restore the original date. Thus, all modified files can be retrieved whenever needed (Listing 10.6).

```
(Linux):# find -newer /root/Install_Date -print
/etc/profile
/etc/printcap
```

**Listing 10.6** Finding all the files modified after installation.

Several current distributions can be updated to a new version without problems and a reinstallation. Nevertheless, this can still be a sensible way to create a backup of one’s adaptations. All modified files could also be transferred to a new computer and be adapted there. Often, however, it is sufficient to know which files have been modified to learn more about the system.