# 822 Part IV: Fedora RHEL Network and Server Setup

![](bbox=[0.118, 0.076, 0.842, 0.365])

Figure 19-2: Manage your multiple folders in SquirrelMail.

If you need more information about configuring mailman, there are places to go. Check the mailman Web site at http://www.gnu.org/software/mailman/mailman.html. Also view README files in `/usr/share/doc/mailman-*.

> NOTE: If you used mailman in an earlier version of Fedora or Red Hat Linux, note that the mailman installation directory has moved from `/var/mailman` to `/usr/lib/mailman`. If you made any changes to files in the `/var/mailman` directory, you need to move those files to the `/var/lib/mailman` directory after you upgrade the mailman software package.

The following is a brief procedure for configuring a discussion list using mailman:

+   1. Install the mailman RPM from the Fedora DVD or type `yum install mailman`.

+   2. Start your web server (if it's not already running) as follows:

```
# service httpd start
# chkconfig httpd on
```

+   3. Create a password for your user as follows:

```
/usr/lib/mailman/bin/mmsetpass
New site password: *****
Again to confirm password: *****
```

+   4. Edit the `/usr/lib/mailman/Mailman/mm_cfg.py` file and change the `DEFAULT_URL_HOST` and `DEFAULT_EMAIL_HOST` values. For example, the hostname of the computer I'm configuring my mail list is `toys.luinuxtoys.net`. The values would appear as follows:

```
DEFAULT_EMAIL_HOST = 'toys.luinuxtoys.net'
DEFAULT_URL_HOST DEF = 'toys.luinuxtoys.net'
```