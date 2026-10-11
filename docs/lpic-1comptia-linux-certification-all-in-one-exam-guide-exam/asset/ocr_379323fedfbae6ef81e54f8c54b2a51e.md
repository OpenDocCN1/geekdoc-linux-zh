* `/etc/login.defs` This file contains values that can be used for the GID and UID parameters when creating an account with useradd. It also contains defaults for creating passwords in /etc/shadow. A portion of this file follows:

```
```text
ws1:/ # cat /etc/login.defs
# /etc/login.defs - Configuration control definitions for putils package.
# Comment lines (lines beginning with '#') and blank lines are ignored.
# Please read the manual page for more information (login.defs.5).
DEFAULT_HOME                 yes
...
PASS_MAX_DAYS         99999
PASS_MIN_DAYS            0
PASS_WARN_AGE            7
SYSTEM_UID_MIN          100
SYSTEM_UID_MAX          499
UID_MIN                1000
UID_MAX                60000
SYSTEM_GID_MIN           100
SYSTEM_GID_MAX           499
GID_MIN                 1000
GID_MAX                60000
UMASK                     022
GROUPADD_CMD         /usr/sbin/groupadd.local
USERADD_CMD        /usr/sbin/useradd.local
USERDEL_PRECMD     /usr/sbin/userdel-pre.local
USERDEL_POSTCMD    /usr/sbin/userdel-post.local
ws1:/ #
```
```

Notice that this file specifies default values for the fields we reviewed earlier in/etc/shadow for each user account. It also specifies defaults used when useradd is assigning a UID to a new account. Remember that, earlier in this chapter, we noted that SUSE Linux starts UIDs at 1000 while Fedora starts UIDs at 500. This file is where this behavior comes from. It also defines the UID number range for system user accounts. It also defines which executable to run when you run useradd or userdel from the shell prompt. If you don't like the defaults, you can always edit this file to match your preferences.

* `/etc/skel` The useradd command copies files from the skeleton directory (/etc/skel by default) into a newly created home directory when you create a new user. Typically, /etc/skel also contains several user configuration files, such as .bashrc and .profile. Here is an example:

```
```text
ws1:/ # ls /etc/skel
.bash_history bin        .fonts    .mozilla       public_html    .xim.template
.bashrc       .emacs     .inputrc  .profile       .vimrc         .xintrc.template
ws1:/ #
```
```

You can add any files and directories to this directory that you want each and every user to have by default when their account is created on the system.

You can override these defaults when running useradd by specifying a list of options in the command line. You can use the following:

+   * `-c` Includes the user's full name