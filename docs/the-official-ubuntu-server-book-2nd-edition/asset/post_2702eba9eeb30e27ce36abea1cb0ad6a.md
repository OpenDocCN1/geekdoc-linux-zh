
The first word will be a # symbol marking the line as a comment or else either deb or deb-src. This specifies whether the repository is a source package repository or a binary package repository. The second item is the location in the form of a URI. The third item is the name of the distribution or, as it might more accurately be described, the distribution version. In the previous example, this distribution version is lucid, which refers to the Ubuntu release of the Lucid Lynx. The remaining arguments are the lists of the components. The components provided in the core Ubuntu repositories are detailed in the following section.

An example will help illustrate the process of adding a repository. If I want to install a version of Bazaar that is always the latest released version, I will need to do this from outside the default Ubuntu repositories, which will only be updated based on the Ubuntu release cycle. Luckily, the Bazaar developers provide their own “Personal Package Repository”—a subject I’ll come back to at the end of this chapter. On their Web site, they provide the deb and deb-src lines that I can simply drop into my sources.list:

```
deb http://ppa.launchpad.net/bzr/ubuntu lucid main
deb-src http://ppa.launchpad.net/bzr/ubuntu lucid main
```

If I update, I am first greeted by an error that claims that I do not have the correct cryptographic key to verify that the packages in the repository are really coming from the Bazaar developers:

```
W: GPG error: http://ppa.launchpad.net lucid Release: The following
signatures couldn't be verified because the public key is not
available: NO_PUBKEY FE8956A73C5EE1C9
```

I can easily install that by downloading the key from a trusted source like the PPA providers’ Web site and saving it into a file (called /tmp/keyfile in the example below), verifying that is correct, and adding to the package manager’s key database with a command such as

```
apt-key add - < /tmp/key
OK
```

The apt-key manual page gives more details on how keys for repositories can be managed with this useful command.

## Ubuntu Default Repositories

The vast majority of packages that you will need have been packaged for Ubuntu. This is because, leveraging the work of Debian, Ubuntu provides access to a large majority of the most popular pieces of free software as packages in their own repositories.

These tens of thousands of packages are separated into a series of different sections or components. You can toggle these on and off by including them in the list of components in your sources.list. Because these have important consequences for the level of support you will receive for your software, it is worth understanding these different components so that you can decide from which areas you want to pull software. Available components on the Ubuntu server include main, restricted, universe, and multiverse. The following descriptions are adapted from the component descriptions on the Ubuntu Web site.

- **Main**
  The main distribution component contains applications that are free software, can freely be redistributed, and are fully supported by the Ubuntu team. These include the most popular and most reliable open source applications available, much of which is installed by default when you install Ubuntu. Software in main includes a hand-selected list of applications that the Ubuntu developers, community, and users feel are important and that the Ubuntu security and distribution teams are willing to support. When you install software from the main component, you are assured that the software will come with security updates and technical support.

- **Restricted**
  The restricted component is reserved for software that is very commonly used and that is supported by the Ubuntu team even though it is not available under a completely free license. Please note that it may not be possible for Ubuntu to provide complete support for this
software since the Ubuntu team is unable to fix the software but can only forward problem reports to the actual authors.

- **Universe**
  In universe one can find almost every piece of open source software and software available under a variety of less-open licenses, all built automatically from a variety of public sources. All of this software is compiled against the libraries and using the tools that form part of main, so it should install and work well with the software in main, but *it comes with no guarantee of security fixes and support*.

- **Multiverse**
  The multiverse component contains software that is not free, which means the licensing requirements of this software do not meet the “main” component license policy. The onus is on you to verify your rights to use this software and comply with the licensing terms of the copyright holder. This software is not supported and usually cannot be fixed or updated. Use it at your own risk.

## Using Other Repositories

As you saw when I added the Bazaar repository several sections ago, users will still sometimes want to make use of a variety of outside repositories beyond what is provided in Ubuntu. For example, users might want to install new versions of particular applications or libraries from the development release of Ubuntu but might not want to upgrade all of their packages to the latest version.

The quasi-official “backports” repository in Ubuntu is a useful resource. It contains versions of software from the development version of Ubuntu that have been backported to install cleanly on stable versions of Ubuntu. You can add the backports by installing a DEB package by hand in a one-by-one with dpkg or by adding an extra line to your sources.list. Information on doing both can be found on the Ubuntu Web site at https://help.ubuntu.com/community/UbuntuBackports.

One reason that many users choose to go the à la carte method—that is, the method of downloading packages by hand and installing them with dpkg—as opposed to just adding the repository is because of a limitation in the
