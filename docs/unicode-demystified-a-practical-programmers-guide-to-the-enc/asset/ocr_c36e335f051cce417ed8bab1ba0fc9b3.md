# Red Hat Network Alert Notification Tool Icon Menu

| Check for updates | Runs up2date (page 939) in the background to check for updates. The green icon with arrows on the Red Hat Network Alert Notification button shows you that your system is communicating with the RHN server. |
| Launch up2date | Runs up2date (page 939) in the foreground, opening a series of windows that do not give you many options. |
| Configuration | Opens a series of windows that display the Terms of Service, allows you to configure a proxy, and checks for updates. |

# up2date: RHN Update Agent

The up2date utility is the workhorse at the client end of RHN: Its basic function is to download rpm packages from the RHN server. It works with many files and directories, in graphical and character-based modes, and has many options.
Of the most important options, --config, generates up2date's system profile file (/etc/sysconfig/rhn/up2date). The up2date-config utility (next section) is a link to up2date with the --config option. You do not normally use this option because up2date itself (creates the RHN system profile) when necessary.
nox option (also up2date-nox) runs up2date in noninteractive, character-based mode. Refer to the up2date man page for more information.

In addition to updating packages that are on your system, up2date can download and install Red Hat packages that are not on your system. Following the user links, the character-based browser program, finds it is not on the system, and confirms that finding with theirs. Then, up2date, with the --whatprovides option, queries RHN to find that the elinks package provides links. Finally, up2date, with an argument of the rpm package to be installed, downloads the package from RHN. In this case up2date installs the package because that the system profile is set up to do. You must run up2date as Superuser to install or upgrade a package.

```
$ ls\dup2date --whatprovides links
elinks-0.3.2-1
$ su
```

Password: