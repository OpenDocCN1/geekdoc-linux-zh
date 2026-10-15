"universe multiverse" components. We highly recommend you have these two components enabled, as they open up a huge collection of software that will enable you to get the most out of this book and Ubuntu itself.

At the bottom of the sources.list file there are usually some deb lines that handle security updates. This has a special URL, security.ubuntu.com, and a special distribution name, dapper-security. This should be left enabled at all times.

If you have made changes to your sources.list file, you must run apt-get update to download the new package information before running any further APT commands.

Before changing your sources.list file, we highly recommend keeping a backup of the original by running this command:

```
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

# Reference

http://www.debian.org/doc/manuals/apt-howto/—The official Debian APT HOWTO manual page.

http://www.apt-get.org/—A list of popular APT repositories.

http://wiki.debian.org/SecureApt—Guide to using strong cryptography with your APT sources.

http://www.debian.org/releases/woody/i386/dselect-beginner—How to get started using dselect for package management.