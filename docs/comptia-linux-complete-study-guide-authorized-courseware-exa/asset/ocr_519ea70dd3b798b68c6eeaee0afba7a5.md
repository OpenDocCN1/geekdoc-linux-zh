# **TABLE 2.6** apt-get Commands (continued)

| Command | Description |
| :--- | :--- |
| check | Checks the package database for consistency and broken package installations. |
| clean | Performs housekeeping to help clear out information about retrieved files from the Debian package database. If you don't use dselect for package management, run this from time to time in order to save disk space. |
| autoclean | Similar to clean, but removes information only about packages that can no longer be downloaded. |

# **TABLE 2.7** Most Useful apt-get Options

| Option | Used with Commands | Description |
| :--- | :--- | :--- |
| -d or --download-only | uprade, dselect-upgrade, install, source | Downloads package files but doesn't install them. |
| -f or --fix-broken | install, remove | Attempts to fix a system on which dependencies are unsatisfied. |
| -m, --ignore-missing, or --fix-missing | uprade, dselect-upgrade, install, remove, source | Ignores all package files that can't be retrieved (because of network errors, missing files, or the like). |
| -q or --quiet | All | Omits some progress indicator information. May be doubled (for instance, -qq) to produce still less progress information. |
| -s, --simulate, --just-print, --dry-run, --recon, or --no-act | All | Performs a simulation of the action without actually modifying, installing, or removing files. |
| -y, --yes, or --assume-yes | All | Produces a "yes" response to any yes/no prompt in installation scripts. |