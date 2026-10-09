
to walk through it here. You should be familiar with the customizations you've made to your system, so nothing should surprise you. If anything looks unfamiliar, refer to Chapter 14.

Reboot, and your base system is fully upgraded!

## Customizing Mergemaster

Once you’ve run mergemaster a few times you’ll realize that certain files always annoy you. Mergemaster will always complain about your customized */etc/motd* and */etc/printcap*. You’ll probably wind up typing -f or -u every single time. You can set your preferred options in *$HOME/.mergemasterrc*, as documented in *mergemaster*(8). While you should read the man page for the complete list, here are the options I use most often.

### Ignoring Files

Certain files you don’t want mergemaster to even bother examining. Your organization’s */etc/motd* will never match that in the *FreeBSD* distribution. Neither will your custom printer configuration, your *snmpd.conf*, or your tailored *sshd_config*. To have mergemaster skip these files, list them in *IGNORE_FILES*.

```
IGNORE_FILES='/etc/motd /etc/printcap'
```

I don’t list the password or group file here because sometimes *FreeBSD* introduces new users.

### Auto Install New Files

If you want mergemaster to automatically install files present in the new version of *FreeBSD* but not on the system yet, set *AUTO_INSTALL*.

```
AUTO_INSTALL=yes
```

This is equivalent to the *-i* flag.

### Autoupdate Unchanged Files

Different versions of FreeBSD have similar files. Some files are almost identical, differing only by the line containing version control information. You can tell mergemaster to automatically update files that differ only by the version control information by using the FREEBSD_ID option.

```
FREEBSD_ID=yes
```

This is the same as the -f flag.

### Autoupdate Unedited Files

You can tell mergemaster to update files that haven't been edited since they were installed. The FreeBSD team changes /etc/ files when it wants to change how the system behaves. While many of those changes might be irrelevant to you, a few might give you trouble. If you want to blindly update everything you haven't touched, set AUTO_UPGRADE.

```
AUTO_UPGRADE=yes
```

This is equivalent to the -u option.

### Update Databases

FreeBSD builds databases from /etc/master.passwd, /etc/services, and so on. If you update these files, you also need to update the corresponding databases. Mergemaster asks you at the end of each run if you want to run these updates. Tell mergemaster always to run the updates by setting RUN_UPDATES.

```
RUN_UPDATES=yes
```

You can find other options in mergemaster(8).

### Upgrades and Single-User Mode

According to the instructions, several parts of the upgrade must be done in single-user mode. Many users consider this an annoyance or even a handicap. FreeBSD programs are just files on disk, aren't they?

Common sense says that you can just copy them to the disk, reboot, and be done with it.

Here’s yet another instance where your common sense is trying to run your mouth. On rare occasions, the FreeBSD team needs to make some low-level changes in the system that require running the install in single-user mode. You can have conflicts where vital programs won’t run when installed in multiuser mode. This is rare, but if it happens with /bin/sh, you’re in a world of hurt. You have a very straightforward recovery route if that happens: remove the hard drive from the server, mount it in another machine, boot the other machine, and copy your data off the destroyed system before formatting and reinstalling. Or, you can boot from the installation media and demonstrate your amazing sysadmin skills.5

Running in multiuser mode can cause other upgrade problems, such as subtle races, symbol issues, and innumerable other headaches. You can choose to upgrade in multiuser mode, but don’t complain if your system has a problem.

It’s perfectly safe to build your new world in multiuser mode. You can even build and install your new kernel in multiuser mode. Once you start installing the userland, however, you must be in single-user mode and running on your upgraded kernel.

## NFS AND UPGRADES

Have a lot of machines to update? Look at NFS, which we discussed in Chapter 13. Build world and all your kernels on a central, fast machine, and then export /usr/src and /usr/obj from that system to your other clients. Running make installkernel and make installworld from those NFS exports saves build time on all your other machines and guarantees that you have the same binaries on all your FreeBSD boxes.

## Shrinking FreeBSD

What's the point of having all this source code if you can't customize your operating system? FreeBSD not only gives you the source code; it provides ready-to-turn knobs to easily customize your FreeBSD build.

These options can be set in either `/etc/make.conf` (see Chapter 16) or `/etc/src.conf`. Settings in `src.conf` apply only to building the FreeBSD source, while `make.conf`'s settings apply to all source code building. The full list of `src.conf` options are documented in `src.conf(5)`, but they all follow a standard pattern.

Each of these options starts with either `WITHOUT_` or, in a few cases, `WITH_` and then names a specific subsystem. For example, the `WITHOUT BHYVE` option turns off building or installing the `bhyve(8)` hypervisor. The `WITHOUT_INETD` option turns off building the `inetd(8)` daemon (see Chapter 20). The `WITHOUT_INET6` option turns off IPv6. If you want to shrink your FreeBSD install, chop out everything you don't need.

The build system checks to see whether any of these variables are defined to any value at all. This means that even if you set one of these to `NO`, the mere presence of the option activates the option. Don't go copying all of these to `src.conf` and setting them all to `NO` because you'll disable building a great big bunch of the system.

In most cases, adding these `WITHOUT_` options includes the removed systems in the `make delete-oid` checks. If you decide that your system doesn't need `bhyve(8)`, for example, the upgrade not only doesn't build a new `bhyve` binary but also offers to remove the existing one from the installed system. If you're not building a piece of software, you're better off removing it entirely as opposed to leaving the old version lingering on the system.

## Packages and System Upgrades

Operating system upgrades are great, except for the part where nobody cares.<sup>6</sup> Base operating system updates are necessary, but most people don't really care about using the base system. They care about using software that runs on the base system. And that software is prone to the same flaws as every other program. You need to upgrade it. Chapter 15 discusses upgrading packages in general, but let's talk about what happens when you upgrade the operating system underneath the packages.

The common issues with packages and system upgrades normally boil down to shared libraries. If you're upgrading FreeBSD major releases—say, from FreeBSD 12 to FreeBSD 13—you'll need to reinstall all of your packages.

Start by upgrading pkg(8) itself, using the -f flag to pkg upgrade. If the upgrade broke pkg(8) itself, you'll need to use pkg-static(8). This contains key pkg(8) functions, but it's a static binary.

```
# pkg-static upgrade -f pkg
```

This will bootstrap you into the current package tools. Now you can force a redownload and reinstall of all packages.

```
# pkg upgrade -f
```

Once you've upgraded everything you built from packages, rebuild anything you built from ports. I really hope you installed your ports via poudriere, though.

## Updating Installed Ports

If you use portsnap to update your ports tree, anything you install from now on will be the latest version. But what about your previously installed applications? FreeBSD tracks all sorts of dependency information between add-on packages, and often updating one program will impact dozens of others. This is a royal pain to manage. Wouldn't it be nice to just say, “Update my Apache install,” and have FreeBSD manage the dependencies for you? There's a few ways to solve this issue.

The best way is not to use the ports tree on a production host. Build a private repository with poudriere instead (see Chapter 16), and have
