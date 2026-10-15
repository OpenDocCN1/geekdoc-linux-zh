# apt-get automation

You can run apt-get on a regular schedule from cron. Even if you don't install packages automatically, you may want to run apt-get update regularly to keep your package summaries up to date.

# apt-get dist-upgrade

downloads and installs new versions of any packages that are currently installed on the local machine. dist-upgrade is similar to upgrade but has slightly more intelligent dependency handling. dist-upgrade may want to delete some packages that it views as irreconcilably incompatible with the upgraded system, so be prepared for potential surprises.

If you really want to play with fire, have machines perform the upgrade in an unattended fashion by using the -yes option. It answers any confirmation questions that apt-get might ask with an enthusiastic "Yes!" Be aware that some updates, such as kernel packages, may not take effect until after a system reboot.

It's probably not a good idea to perform automated upgrades directly from a distribution's mirror. However, in concert with your own APT servers, packages, and release control system, this is a perfect way to keep clients in sync. A quickie shell script like the following keeps a box up to date with its APT server:

```
#!/bin/sh
apt-get update
apt-get -yes dist-upgrade
```

Call this script from a cron job if you want to run it nightly. You can also refer to it from a system startup script to make the machine update at boot time. See Chapter 9, Periodic Processes, for more information about cron; see Chapter 3, Booting and Shutting Down, for more information about startup scripts.

If you run updates out of cron on many machines, it's a good idea to use time randomization to make sure that everyone doesn't update at once. The short Perl script on page 727 can help with this task.

If you don't quite trust your source of packages, consider automatically downloading all changed packages without installing them. Use apt-get's --download-only option to request this behavior, then review the packages by hand and install the ones you want to update. Downloaded packages are put in /var/cache/apt, and over time this directory can grow to be quite large. Clean out the unused files from this directory with apt-get autoclean.

# yum: release management for RPM

yum, the Yellowdog Updater, Modified, is a metapackage manager based on RPM.1 It may be a bit unfair to call yum an apt-get clone, but it's thematically and implementationally similar, although cleaner and slower in practice. yum is the official package management system for Red Hat Enterprise Linux and comes