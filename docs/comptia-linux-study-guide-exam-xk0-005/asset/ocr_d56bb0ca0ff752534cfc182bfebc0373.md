# TABLE 13.3  The rpm command actions

| Action | Description |
|---|---|
| `-b` | Builds a binary package from source files |
| `-e` | Uninstalls the specified package |
| `-F` | Upgrades a package only if an earlier version already exists |
| `-i` | Installs the specified package |
| `-q` | Queries if the specified package is installed |
| `-U` | Installs or upgrades the specified package |
| `-V` | Verifies if the package files are present |

```
$ sudo rpm -Uvh zsh-5.0.2-31.el7.x86_64.rpm  
Preparing...                                ##################################### [100%]  
Updating / installing...  
1:zsh-5.0.2-31.el7        ##################################### [100%]  
$
```

You use the `-q` action to query the package management database for installed packages:

```
$ rpm -q zsh  
zsh-5.0.2-31.el7.x86_64  
$
```

If you need to remove an installed package, just use the `-e` action:

```
$ sudo rpm -e zsh  
$ sudo rpm -q zsh  
package zsh is not installed  
$
```

The `-e` action doesn’t show if it was successful, but it will display an error message if something goes wrong with the removal.

# # Understanding Repositories

The dpkg and rpm commands are useful tools, but they both have their limitations. If you’re looking for new software packages to install, it’s up to you to find them. Also, if a package depends on other packages to be installed, it’s up to you to install those packages first and in the correct order. That can become somewhat of a pain to keep up with.