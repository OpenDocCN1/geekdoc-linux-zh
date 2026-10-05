# GUIDED EXERCISE

# ENABLING YUM SOFTWARE REPOSITORIES

In this exercise, you will configure your server to get packages from a Remote Yum repository,
then update or install a package from that repository.

# ### OUTCOMES

You should be able to configure a system to obtain software updates from a classroom server
and update the system to use latest packages.

# ### BEFORE YOU BEGIN

Log in as the student user on workstation using student as the password.

From workstation run the lab software-repo start command. The command runs
a start script that determines whether the host servera is reachable on the network. The
script also ensures that the yum package is installed.

```
[student@workstation -]$ lab software-repo start
```

+   1. Use the ssh command to log in to servera as the student user.

```
[student@workstation -]$ ssh student@servera
[student@servera -]$
```

+   2. Use the su - to switch to root at the shell prompt.

```
[student@servera -]$ su -
Password: redhat
[root@servera -]$
```

+   3. Configure software repositories on servera to obtain custom packages and updates from
the following URL:

+   * Custom packages provided at http://content.example.com/rhel8.0/x86_64/
rhsa-pratico/rht
* Updates of the custom packages provided at http://content.example.com/
rhel8.0/x86_64/rhsa-practice/errata

3.1. Use yum-config-manager to add the custom packages repositories.

```
[root@servera -]$ yum-config-manager \
> --add-repo "http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht"
Adding repo from: http://content.example.com/rhel8.0/x86_64/rhsa-practice/rht
```