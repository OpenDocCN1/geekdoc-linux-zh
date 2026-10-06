
Click Your RHN, Entitlements, and then the Service Entitlements tab. You should see your profilename in the Name column toward the bottom of the frame. Use the drop down list in the Entitled column to select Basic for your system. Click Update Entitlements.

- Check for updates. Run update2, or choose Red Hat Network Alert Notification Icon menu: Check for updates (page 939) to see if the RHN server downloads files or exchanges information with your system. You can also give the command `update2 --list` to see whether any packages are available for your system, thereby testing your connection with the RHN server.

You can start the flow of updates from your system or from the Web Site. From your system log in, click Systems>Systems List>Detailed view, click UPDATE NOW on the line with profile on it, and click Confirm Update For This System. In this case the next time the rhnsd daemon on your system contacts the RHN server, you will get updates per the RHN system profile (installed or not, left on the system or source code or not, and so on).

## Red Hat Network Alert Notification Tool

The Red Hat Network Alert Notification Tool can take care of everything you need to set up, run, and administer your RHN account. The Red Hat Network Alert Notification Tool is represented by a round button on both the GNOME and KDE Main panel. It shows one of four icons:

- Blue with a check mark indicates that all is well: There are no pending downloads.
- Red with an exclamation point indicates that files need to be downloaded. Click the button.
- Green with half arrows pointing left and right indicates that the system is communicating with the RHN server.
- Grey with a question mark indicates that there has been an error. Click the icon to display the error message.

If the button is not on the Main panel, run rhn-alert-gui from Run Program on the GNOME menu or Run Command on the K menu to display it. Table 17-5 describes the selections on the Red Hat Network Alert Notification Tool panel icon (right click),

## Red Hat Network Alert Notification Tool Icon Menu

| Option | Description |
| :--- | :--- |
| Check for updates | Runs up2date (page 939) in the background to check for updates. The green icon with arrows on the Red Hat Network Alert Notification button shows you that your system is communicating with the RHN server. |
| Launch up2date | Runs up2date (page 939) in the foreground, opening a series of windows that do not give you many options. |
| Configuration | Opens a series of windows that display the Terms of Service, allows you to configure a proxy, and checks for updates. |

## up2date: RHN Update Agent

The up2date utility is the workhorse at the client end of RHN: Its basic function is to download rpm packages from the RHN server. It works with many files and directories, in graphical and character-based modes, and has many options.

Of the most important options, `--config`, generates up2date's system profile file (/etc/sysconfig/rhn/up2date). The up2date-config utility (next section) is a link to up2date with the --config option. You do not normally use this option because up2date itself (creates the RHN system profile) when necessary.

The `nox` option (also up2date-nox) runs up2date in noninteractive, character-based mode. Refer to the up2date man page for more information.

In addition to updating packages that are on your system, up2date can download and install Red Hat packages that are not on your system. Following the user links, the character-based browser program, finds it is not on the system, and confirms that finding with theirs. Then, up2date, with the `--whatprovides` option, queries RHN to find that the elinks package provides links. Finally, up2date, with an argument of the rpm package to be installed, downloads the package from RHN. In this case up2date installs the package because that the system profile is set up to do. You must run up2date as Superuser to install or upgrade a package.

```bash
$ ls up2date --whatprovides links
elinks-0.3.2-1
$ su
```
Password:

## up2date elinks

Fetching package list for channel: redhat-linux-i386-8.0...
###########################################################

Fetching Obsoletes list for channel: redhat-linux-i386-8.0...
###########################################################

Fetching rpm headers...

Testing package set / solving RPM inter-dependencies...
############################################################ Done.
elinks-0.3.2-1.i386.rpm: ######################################## [100%]

Preparing
############################################################ [100%]

Installing...
1:elinks ########################################################### [100%]

## up2date-config: Configures the RHN Update Agent

The RHN Update Configuration Tool, up2date-config, sets 18 sets of the parameters in your RHN system profile. You can run up2date-config from a command line, but it is not usually required because up2date-config itself [note: original text error, likely "is called"] as necessary, usually the first time you run it. In a graphical environment, this tool displays a window with three tabs: General, Retrieval/Installation, and Package Exceptions (Table 17-6).

## Red Hat Network Configuration Window

| General Network Settings | Description |
| :--- | :--- |
| Select a Red Hat Network Server to use | This box is already filled for you. Do not change it unless you have reason to do so. |
| If you need a HTTP proxy, enter it here in the format HOST:PORT e.g. squid.mysite.org 3128 | |
| Enable HTTP Proxy | Enter your HTTP proxy server (page 397) in the required format if you need to use a proxy server. |

> 18. The up2date-config command is a link to up2date. When using this link, up2date determines it was called as up2date-config and takes the same actions as it would have been called directly with the --configure option.

## Red Hat Network Configuration Window (Continued)

| Option | Description |
| :--- | :--- |
| Use Authentication | Select Use Authentication and fill in the Username and Password text boxes when your proxy server requires authentication. These spaces are for the proxy server, not for your RHN username and password. |
| Retrieval/Installation | | |
| Package Retrieval Options | |
| Do not install packages after retrieval | Download, but do not install packages. You will need to install the new packages manually. |
| Do not upgrade packages when configuration file has been modified | Do not download or install packages that have been customized. This option is not necessary unless |
| Retrieve RPM along with binary | Download the source code (src) file in addition to the binary that is be installed. RHN does nothing with the source except download it. |
| Package Verification Options | |
| Use GPG to verify package integrity | Uses Red Hat's signature to verify the authenticity of the files you are downloading. This is a critical link in the | |
| Package Installation Options | |
| After installation, keep binary packages on disk | Normally the rpm files are removed once they have installed on your system. Select this option if you want |
| Enable RPM rollbacks (allows "undo" but requires additional storage space) | By using extra disk space, RHN can store information so that it can uninstall |

## Red Hat Network Configuration Window (Continued)

| Table 17-6 | Description |
| :--- | :--- |
| Override version stored in System Profile | Downloads and installs packages for a version of Red Hat that specify in the text box, overriding the version number that is stored in your system profile. |
| Package storage directory | Specifies a directory to store the downloaded files. In default they are stored in `/var/spool/update2`. |
| Package Exceptions | Specifies packages and files that you do not want to download. These names can include wildcard characters. |
| Package Names to Skip | By default `kernel*` appears in this list box, meaning that rpm packages whose names begin with the letters kernel will be be downloaded. Installing a new kernel is an important event, and Red Hat assumes that you do not want this to happen without your knowledge. Use the Add, Edit, and Remove buttons to adjust the list box to your requirements. Normally you do not have to make any changes here. |
| File Names to Skip | Similar to Package Names to Skip except you can specify names that you want to skip |

daemon is a background service that periodically queries the RHN server to find out whether new packages need to be downloaded. This daemon is one of the keys to RHN security; it is the component that initiates contact with the RHN server so that the server never has to initiate with your system. Refer to service: Configures Services I on page 945 to start, stop, or display the status of `rhnsd` immediately and to `redhat-config-services`: Configures Services II on page 946 to start or stop `rhnsd` at specified runlevels.

# System Operation

This section covers the basics of how the system functions and how you can make intelligent decisions as a system administrator. This section does not cover every aspect of system administration in the depth necessary to set up or modify all system functions. It provides a guide to bringing a system up and keeping it running from day to day. Subsequent sections of this chapter and Part III of this book describe many of the system administration files and utilities in detail.
