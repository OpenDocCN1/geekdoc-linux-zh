from the finicky remote server, one thing I verify is the package integrity.

```
# pkg check -s rsync
Checking rsync:   0%
rsync-3.1.2_6: checksum mismatch for /usr/local/bin/rsync
Checking rsync: 100%
```

Either the disk is failing or someone has mucked with my rsync(1) binary. As this system uses self-healing ZFS, there’s gonna be a paddling.

You could uninstall and reinstall the package, but that might trigger changes depending on which packages require the package you’re updating. Also, as discussed earlier, this particular package is special. I don’t want pkg to upgrade the package to the newest version. Instead, I want to force pkg to reinstall the current package from the package cache. Use the -f flag to pkg install. While it updates the repository database, it reinstalls the cached package. If the package is locked, you must unlock it first.

```
# pkg unlock -y rsync
Unlocking rsync-3.1.2_6
# pkg install -fy rsync
--snip--
[1/1] Reinstalling rsync-3.1.2_6...
[1/1] Extracting rsync-3.1.2_6: 100%
# pkg lock -y rsync
```

My precious rsync is restored.

Check the integrity of all your packages by running pkg check -saq. It produces no output unless something has changed, so you could schedule it via cron (see Chapter 20).

# ## Dependency Problems

If someone really tries, they can delete packages that other packages depend on. Use the -d flag of pkg check to identify and fix missing dependencies.

```
# pkg check -d emacs-nox11
Checking emacs-nox11: 100%
emacs-nox11 has a missing dependency: gnutils
emacs-nox11 is missing a required shared library: Qlibgnutls.so.30
```