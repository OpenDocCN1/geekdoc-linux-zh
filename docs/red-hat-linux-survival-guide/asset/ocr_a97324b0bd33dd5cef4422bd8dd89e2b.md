```
#
# Require password before chfn/chsh can make
# any changes.
#
CHFN_AUTH  yes

#
# Don't allow users to change their "real name"
# using chfn.
#
CHFN_RESTRICT  yes

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. Owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD  /usr/sbin/userdel_local

#
# If useradd should create home directories for
# users by default on RH systems, we do. This option is
# ORed with the -m flag on useradd command line.
#
CREATE_HOME  yes
```

Because the comments in this file are sufficient to explain the configuration details, they are not discussed any further here.

# Saving Disk Space
with Disk Quotas

Disk space on a multiuser system can be quite a scarce resource. My experience has been that as soon as you plug in a new drive with lots of space, users tend to use it up quite rapidly. So, the more space you add, the more space you need! The best way to ensure that you have enough disk space for your system is to enforce disk quotas. The following sections explain how.