```
return 0
else
    return 1
}
```

```
################################################################################
# wait_for_user()                                                               #
# Purpose: Wait for the user to respond if not a headless system                  #
################################################################################
wait_for_user()
```

```
{
# Wait for the user by default
    [ "$HEADLESS=0" = "0" ] && read ENTER
    return 0
}
```

```
################################################################################
# is_true()                                                                       #
# Purpose: Utility to test if a variable is true | yes | 1                          #
################################################################################
is_true()
```

```
{
    [ "$1" = "1" ] || [ "$1" = "yes" ] || [ "$1" = "true" ] || [ "$1" = "y" ] | |
    [ "$1" = "t" ]
}
```

```
# End /etc/lsb/init-functions
```

# D.3. /etc/rc.d/init.d/mountvirtfs

```
#!/bin/sh
################################################################################
# Begin mountvirtfs
# Description : Mount proc, sysfs, and run
# Authors : Gerard Beekmans - gerard@linuxfromscratch.org Lucas - dj@linuxfromscratch.org
# Update : Bruce Dubbs - bdbubbs@linuxfromscratch.org
# Version : LFS 7.0
################################################################################
```

```
### BEGIN INIT INFO
# Provides: mountvirtfs
# Required-Start:
# Should-Start:
# Required-Stop:
# Should-Stop:
# Default-Start: S
```