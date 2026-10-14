Removing a package is similarly simple. If I decide to remove most, I can do so by running

```
# aptitude remove most
```

In this case, libslang2 will not be removed (since I have not asked for it to be removed). If I were instead to try to remove libslang2, Aptitude would prompt me and explain that removing libslang2 would also require removing all of the packages that depend on it—on this system, that would just be most, but for other packages or on other systems there could be quite a few packages. This type of dependency management means that, for example, users should not (and cannot easily) remove core or essential packages. Extra "unused" packages can be removed using the command apt-get autoremove.

Finally, while these examples both used Aptitude, the installation and removal of packages can also be done with the lower-level tool dpkg. In fact, in both cases Aptitude is simply calling dpkg on the downloaded package files behind the scenes. Aptitude—or apt-get—will always download packages and work out dependencies before turning to dpkg. If you have already installed existing dependencies, you can install a DEB directly with dpkg by using the -i command and passing the package filename as an argument. For example, if I were given a DEB file for most, I could install it with a command like this:

```
$ dpkg -i most_5.0.0a-1_1386.deb
```

dpkg will check dependencies and produce an error if there are missing dependencies but will not automatically download or install packages since it does not contain the functionality to do this. I could uninstall most with dpkg with the command dpkg -r most.

# Manipulating Installed Packages

dpkg provides dozens of methods of querying, searching, and manipulating installed packages. It contains a database of information about packages