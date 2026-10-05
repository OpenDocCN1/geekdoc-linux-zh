
# GUIDED EXERCISE

## ENABLING YUM SOFTWARE REPOSITORIES

In this exercise, you will configure your server to get packages from a Remote Yum repository,
then update or install a package from that repository.

### OUTCOMES

You should be able to configure a system to obtain software updates from a classroom server
and update the system to use latest packages.

### BEFORE YOU BEGIN

Log in as the student user on workstation using student as the password.

From workstation run the lab software-repo start command. The command runs
a start script that determines whether the host servera is reachable on the network. The
script also ensures that the yum package is installed.

```
[student@workstation -]$ lab software-repo start
```

- 1. Use the ssh command to log in to servera as the student user.

```
[student@workstation -]$ ssh student@servera
[student@servera -]$
```

- 2. Use the su - to switch to root at the shell prompt.

```
[student@servera -]$ su -
Password: redhat
[root@servera -]$
```

- 3. Configure software repositories on servera to obtain custom packages and updates from
the following URL:

  - Custom packages provided at http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht
  - Updates of the custom packages provided at http://content.example.com/rhel8.0/x86_64/rhsa-practice/errata

3.1. Use yum-config-manager to add the custom packages repositories.

```
[root@servera -]$ yum-config-manager \
> --add-repo "http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht"
Adding repo from: http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht
```

# CHAPTER 14 | Installing and Updating Software Packages

3.2. Examine the software repository created by the previous command in the /etc/yum.repos.d. Use the vim command to edit the file and add gpgcheck=0 to disable the GPG key check for the repository.

```
[root@server#]# vim
> /etc/yum.repos.d/content.example.com.rhel8.0_x86_64.rhsa-practice_rht.repo
[content.example.com.rhel8.0_x86_64.rhsa-practice_rht]
name=created by dnf config-manager from http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht
baseurl=http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht
enabled=1
gpgcheck=0
```

3.3. Create the /etc/yum.repos.d/errata.repo file to enable the updates repository with the following content:

```
[rht-updates]
name=rht updates
baseurl=http://content.example.com/rhel8.0/x86_64/rhsa-practice/errata
enabled=1
gpgcheck=0
```

3.4. Use the yum reposolist -a to list all repositories on the system:

```
[root@server -]# yum reposolist all
repo id repo name status
content.example.com.rhel8.0_x86_64.rhsa-practice_rht created by .... enabled: 2
rht-updates rht updates enabled: 2
...output omitted...
```

- 4. Disable the rht-updates software repository and install the rht-system package.

4.1. Use yum-config-manager --disable to disable the rht-updates repository.

```
[root@server -]# yum-config-manager --disable rht-updates
```

4.2. List, and then install, the rht-system package:

```
[root@server -]# yum list rht-system
Available Packages
rht-system.noarch 1.0.0-1 content.example.com.rhel8.0_x86_64-rhsa-practice-rht
[root@server -]# yum install rht-system
Dependencies resolved.

=======================================================================
Package Arch Version Repository Size
=======================================================================
Installing:
rht-system noarch 1.0.0-1 content...._rht 3.7 k
...output omitted... 
Is this ok [y/N]: y
```

![](img/59afb92e10b67a9cecc358a2c65e93b5_525_0.png)

```
...output omitted...
Installed:
rht-system-1.0.0-1.noarch
Complete!
```

4.3. Verify that the rht-system package is installed, and note the version number of the package.

```
[root@servera ~]# yum list rht-system
Installed Packages
rht-system.noarch 1.0.0-1@content.example.com_rhel8.0_x86_64_rhca-practice_rht
```

- 5. Enable the rht-updates repository and update all packages.

5.1. Use yum-config-manager --enable to enable the rht-updates repository.

```
[root@servera ~]# yum-config-manager --enable rht-updates
```

5.2. Use the update command to update all packages.

```
[root@servera ~]# yum update
Dependencies resolved.

=======================================================================
Package Arch Version Repository Size
=======================================================================
Updating:
rht-system noarch 1.0.0-1 content...._rht 3.7 k
...output omitted...
Is this ok [y/N]: y
...output omitted...
Complete!
```

5.3. Verify that the rht-system package is installed and updated.

```
[root@servera ~]# yum list rht-system
Installed Packages
rht-system.noarch 1.0.0-1@content.example.com_rhel8.0_x86_64_rhca-practice_rht
```

- 6. Exit the session.

```
[root@servera ~]# exit
[student@servera -]# exit
[student@workstation -]# exit
```
