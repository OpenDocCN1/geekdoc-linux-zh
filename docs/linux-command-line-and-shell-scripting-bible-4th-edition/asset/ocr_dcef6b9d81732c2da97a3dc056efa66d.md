```
################################################
################################################
#
echo
if [ $debianscore -gt $redhatscore ]
then
    echo "Most likely your Linux distribution is Debian-based."
#
elif [ $redhatscore -gt $debianscore ]
then
    echo "Most likely your Linux distribution is Red Hat-based."
else
    echo "Unable to determine Linux distribution base."
fi
#
echo
#
################################################
#
exit
$
```

Here's the script in action on an Ubutnu system:

```
$ ./PackageMgrCheck.sh
################################################
    This script checks your Linux system for popular
    package managers and application containers, lists
    what's available, and makes an educated guess on your
    distribution's base distro (Red Hat or Debian).
################################################
Checking for Red Hat-based package managers &
application containers...

Checking for Debian-based package managers &
application containers...
You have the basic dpkg utility.
You have the apt package manager.
You have the snap application container.

Most likely your Linux distribution is Debian-based.

$
```