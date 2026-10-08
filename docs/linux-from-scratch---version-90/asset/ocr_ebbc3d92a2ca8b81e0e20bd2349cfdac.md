```
*) 
echo "Usage: ${start|stop|restart}"
  exit 1
fi

exit 0

# End scriptname
```

# D.21. /etc/sysconfig/modules

```
################################################################################
# Begin /etc/sysconfig/modules
#
# Description : Module auto-loading configuration
#
# Authors :
#
# Version : 00.00
#
# Notes : The syntax of this file is as follows:
  <module> [<arg1> <arg2> ...]
#
# Each module should be on its own line, and any options that you want
 passed to the module should follow it. The line delimiter is either
 a space or a tab.
################################################################################

 End /etc/sysconfig/modules
```

# D.22. /etc/sysconfig/createfiles

```
################################################################################
# Begin /etc/sysconfig/createfiles
#
# Description : Createfiles script config file
#
# Authors :
#
# Version : 00.00
#
# Notes : The syntax of this file is as follows:
  if type is equal to "file" or "dir"
    <filename> <permissions> <user> <group>
  if type is equal to "dev"
    <filename> <permissions> <user> <group> <devtype>
      <minor>
#
  <filename> is the name of the file which is to be
  <type> is either file, dir, or dev.
    file creates a new file
    dir creates a new directory
    dev creates a new device
  <devtype> is either block, char or pipe
```