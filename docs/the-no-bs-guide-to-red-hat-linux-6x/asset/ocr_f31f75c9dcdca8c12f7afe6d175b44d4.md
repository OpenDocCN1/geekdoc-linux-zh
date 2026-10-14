know only the package name, not the name of the original package file. Here's how to remove the dogfood package:

```
rpm -e dogfood
```

RPM will tell you if the removal of the package will cause problems for other installed packages. If it will, you may see a message like this:

```
removing these packages would break dependencies:
dogfood is needed by fido-1.0-1
```

If you're sure you know what you're doing, you can add the --nodeps flag, and RPM will skip the dependency checks and uninstall the package anyway.

# UPGRADING AND FRESHENING PACKAGES

Upgrading a package is similar to installing one, but RPM automatically uninstalls existing versions of the package before installing the new one. If an old version of the package is not found, the upgrade option will still install it. (This is different than the freshen option, which will install only if an old version of the package is found.) Note that RPM flags are case sensitive, so be sure to use a capital “U” when upgrading, as in this example:

```
rpm -Uvh panda-2.0-1.i386.rpm
panda
########################################
```

Since RPM performs intelligent upgrading of packages with configuration files, you may see a message like this:

```
saving /etc/panda.conf as /etc/panda.conf.rpmsave
```

RPM is saying that it saved a copy of your original configuration file and installed a new one. You should use diff or a visual inspection to find any differences between the two files to ensure that your customizations are applied to the new version.

# HEY, THAT'S A DOWNGRADE!

If RPM thinks you are trying to upgrade to a package with an older version number, you will see an error message like this: