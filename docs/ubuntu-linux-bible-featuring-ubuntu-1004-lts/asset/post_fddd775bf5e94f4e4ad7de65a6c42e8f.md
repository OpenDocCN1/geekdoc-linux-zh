
# Chapter 19: Adding, Removing, and Updating Software

To start the Software Sources utility on a Ubuntu system, select the System Administration Software Sources menu item. After supplying your password to enable access to this administrative-tool, the Software Sources tool's main dialog displays, as shown in Figure 19-2.

## FIGURE 19-2
The main Software Sources dialog on Ubuntu

![](img/1a233c34336fbf5a85d6eb785e401709_716_0.png)

The main software preferences dialog displays all of the entries in your current /etc/apt/sources.list file, regardless of whether they are commented out or not. Entries that are commented out in the /etc/apt/sources.list file are present, and the checkboxes beside their name are selected. This gives you a convenient overview of all of the valid, standard repository entries in your /etc/apt/sources.list file.

The Software Sources dialog also makes it easy for you to add third-party repositories (often referred to as custom repositories) to the Ubuntu software management tools search for available and updated packages. This is done via the Software Sources application's Other Software tab, shown in Figure 19-3.

To add a new repository or repository component to the list of repositories that your system will search for software packages, select the Third-Party Software tab and click Add. This displays the dialog shown in Figure 19-4.

## Part II: Ubuntu for Desktop Users

## FIGURE 19-3
Adding third-party repositories in the Software Sources tool

![](img/1a233c34336fbf5a85d6eb785e401709_717_0.png)

## FIGURE 19-4
Adding a specific third-party repository

![](img/1a233c34336fbf5a85d6eb785e401709_717_1.png)

Although not particularly elegant, this dialog makes it easy for you to cut-and-paste a repository identification entry from a mail message or browser session where you found it, and automatically add it to your /etc/apt/sources.list file. To return to the dialog shown in Figure 19-3 without adding a new repository entry, click Cancel. To save a new entry after typing it in or cutting and pasting, click "Add Source," which adds the new entry and returns you to the dialog shown in Figure 19-4.

In addition to the Ubuntu Software and Third-Party Software tabs, the Software Sources tool provide three other tabs that let you manage different aspects of your repositories and the update process. These tabs enable you to manage different aspects of system updates and how your system identifies valid repositories, and also enable you to provide some general statistical information about recent updates to your system to help the Ubuntu folks improve the repository configuration and software update tools.

Figure 19-5 shows the Software Sources tool's Updates tab, which enables you to specify your system checks for updates and how it responds to any available updates that it detects.

## FIGURE 19-5
The Updates tab in the Software Sources tool

![](img/1a233c34336fbf5a85d6eb785e401709_718_0.png)

By default, your system automatically checks for updates on a daily basis, displaying an "Available Updates" icon in the GNOME panel at top of your screen when updates are available. If you are using a laptop or other system that only connects to the Internet frequently, you may want to decrease the frequency with which your system checks for updates by selecting another value from the "Check for updates automatically" entry dropdown menu, or disable this item entirely. If you disable this item, you can always check for updates manually using Ubuntu Update Manager, which is discussed later in this chapter in the section. "Using the Ubuntu Update Manager." If you are performing regular checks for updates and are using a system that is often (or always) connected to the Internet, you may want to select the "Download updates in the background, but not install them" option to make sure that packages are already available on your local system when you actually execute the update process. You may want to select the "Install updates without confirmation" option if you want to automatically update security.

## Part II: Ubuntu for Desktop Users

Figure 19-6 shows the Software Sources tool's Updates tab, which enables you to specify your system checks for updates and how it responds to any available updates that it detects.

## FIGURE 19-6
The Updates tab in the Software Sources tool

![](img/1a233c34336fbf5a85d6eb785e401709_719_0.png)

Each package in repository is signed with a key. The Ubuntu management tools will not add packages from unauthorized or unidentifiable repositories. The associated entries in /etc/apt/sources.list point to repositories whose keys are not present in the keying used by the Ubuntu Package Management utilities. See the man page for the apt-key application for information on retrieving and installing keys into this keyring.

Figure 19-7 shows the Authentication tab, which simplifies the process of importing keys into the Ubuntu Package Management.

## FIGURE 19-7
Change notification when exiting the Software Sources

![](img/1a233c34336fbf5a85d6eb785e401709_720_0.png)

# Problems Adding or Accessing Nonstandard Repositories

After modifying your system's /etc/apt/sources.list file, you may find that packages from new repositories you've added aren't actually showing up in the list of available packages. First, make sure that you've updated the list of available repositories and packages, as described at the end of the previous section. This should identify any inaccessible repositories and outright syntax errors in the sources.list file.

Next, when running apt-get update to update your system's idea of repository contents, seeing messages like the following that your system does not have the right authentication keys to add packages from a specified repository to its cache:

```
Ign http://ftp.debian.org lenny Release
Ign http://ftp.debian.org unstable Release
```

Similarly, you may see messages at the end of the output from apt-get update. These are related to the previous messages, which are somewhat less subtle but they explicitly identify missing keys and associated repositories.

```
GPG error: http://ftp.debian.org Testing Release:
The following signatures couldn't be verified because the \\public key is not available:
NO_PUBKEY 010908312D190C5F
GPG error: http://ftp.debian.org unstable Release:
The following signatures couldn't be verified because the \\public key is not available:
NO_PUBKEY 010908312D190C5F
```

In these cases, the associated entries in /etc/apt/sources.list point to repositories whose keys are not present in the keying used by the Ubuntu Package Management utilities.
