# Using Debian Packages

dist-upgrade | Similar to upgrade, but performs "smart" conflict resolution to avoid upgrading a package if doing so would break a dependency.

install | Installs a package by package name (not by package filename), obtaining the package from the source that contains the most up-to-date version.

remove | Removes a specified package by package name.

check | Checks the package database for consistency and broken package installations.

clean | Performs housekeeping to clear out information about retrieved files from the Debian package. If you don't use delect for package management, run this from time to time in order to save disk space.

autoclean | Similar to clean removes information only about packages that can no longer be downloaded.

# **TABLE 2.7** Most-useful apt-get options

| Option | Used with commands | Description |
| --- | --- | --- |
| -d or --download-only | upgrade, dselect-upgrade, install, source | Downloads package files but doesn't install them. |
| -f or --fix-broken | install, remove | Attempts to fix a system on which dependencies are unsatisfied. |
| -m, --ignore-missing, or --fix-missing | upgrade, dselect-upgrade, install, remove, source | Ignores all package files that can't be retrieved (because of network errors, missing files, or the like). |
| -q or --quiet | All | Omits some progress indicator. May be doubled (for instance, -qq) to produce less progress information. |
| -s, --simulate, --just-print, --dry-run, --recon, or --no-act | All | Performs a simulation of the action without actually modifying, installing, or removing files. |