# **aptitude update: SYNCHRONIZES LOCAL PACKAGE INDEXES WITH REPOSITORIES**

The `aptitude update` command synchronizes local package indexes with their corresponding repositories:

```
```
$ sudo aptitude update
Hit http://security.ubuntu.com lucid-security Release.gpg
Ign http://security.ubuntu.com/ubuntu/ lucid-security/main Translation-en_US
Get:1 http://us.archive.ubuntu.com lucid Release.gpg [189B]
Ign http://us.archive.ubuntu.com/ubuntu/ lucid/main Translation-en_US
Ign http://security.ubuntu.com/ubuntu/ lucid-security/universe Translation-en_US
Ign http://security.ubuntu.com/ubuntu/ lucid-security/restricted Translation-en_US
Ign http://security.ubuntu.com/ubuntu/ lucid-security/main Translation-en_US
Ign http://security.ubuntu.com/ubuntu/ lucid-security/multiverse Translation-en_US
Ign http://security.ubuntu.com lucid-security Release

Hit http://us.archive.ubuntu.com lucid-updates/universe Sources
Hit http://us.archive.ubuntu.com lucid-updates/multiverse Packages
Hit http://us.archive.ubuntu.com lucid-updates/multiverse Sources
Fetched 11.1MB in 31s (353kB/s)
Reading package lists... Done
```

```

Current status: 30 updates [+30], 76 new [+33].

After running this command, APT can determine, without accessing repositories, whether installed packages and those in its cache are the most recent versions available.

By default, the `apt cron` script (page 524) synchronizes local package indexes nightly. If this script is running and set to update the package index, you need not run the `update` command. However, you must run this command after you add repositories to `/etc/apt/sources.list` before APT can retrieve files from new repositories.

# **aptitude safe-upgrade AND aptitude full-upgrade: UPGRADE THE SYSTEM**

There are two `aptitude` commands that upgrade all packages on the system: `safe-upgrade`, which upgrades all packages on the system that do not require new packages to be installed, and `full-upgrade`, which upgrades all packages on the system, installing new packages as needed.

The following example uses the `aptitude safe-upgrade` command to upgrade all packages on the system that depend only on packages that are already installed. This command will not install new packages (packages that are not already on the system). Before running this command, run `aptitude update` (page 528) to make sure the local package indexes are up-to-date.

```
```
$ sudo aptitude update
...
$ sudo aptitude safe-upgrade
...
```

```