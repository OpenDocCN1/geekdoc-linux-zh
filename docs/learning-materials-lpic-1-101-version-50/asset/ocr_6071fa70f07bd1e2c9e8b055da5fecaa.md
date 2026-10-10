```
From repo: updates
Summary: Mozilla Firefox Web browser
URL: https://www.mozilla.org/firefox/
License: MPLv1.1 or GPLv2+ or LGPLv2+
Description: Mozilla Firefox is an open-source web browser, designed for standards compliance, performance and portability.
```

# ## Managing Software Repositories

For yum the “repos” are listed in the directory `/etc/yum.repos.d/`. Each repository is represented by a `.repo file, like `CentOS-Base.repo`.

Additional, extra repositories can be added by the user by adding a `.repo file in the directory mentioned above, or at the end of `/etc/yum.conf`. However, the recommended way to add or manage repositories is with the `yum-config-manager` tool.

To add a repository, use the `--add-repo` parameter, followed by the URL to a `.repo` file.

```
# yum-config-manager --add-repo https://rpms.remirepo.net/enterprise/remi.repo
Loaded plugins: fastestmirror, langpacks
adding repo from: https://rpms.remirepo.net/enterprise/remi.repo
grabbing file https://rpms.remirepo.net/enterprise/remi.repo to /etc/yum.repos.d/remi.repo
repo saved to /etc/yum.repos.d/remi.repo
```

To get a list of all available repositories use `yum repolist all`. You will get an output similar to this:

```
# yum repolist all
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: mirror.ufscar.br
 * epel: mirror.glob0.com
 * extras: mirror.ufscar.br
 * updates: mirror.ufscar.br
repo id             repo name                          status
updates/7/x86_64    CentOS-7 - Updates                   enabled:   2,500
updates-source/7    CentOS-7 - Updates Sources           disabled
```

**disabled repositories** will be ignored when installing or upgrading software. To enable or disable a repository, use the `yum-config-manager` utility, followed by the repository id.