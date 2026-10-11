Table 6.1. Verify-mode command syntax and options.
`rpm -V (or --verify, or -y) Options`

| Package Selection Options | Section |
| :--- | :--- |
| `pkg1...pkgN` Verify named package(s) | 6.3.1 |
| `-p <file>` Verify against package file <file> | 6.3.4 |
| `-f <file>` Verify package owning <file> | 6.3.3 |
| `-a` Verify all installed packages | 6.3.2 |
| `-g <group>` Verify packages belonging to group <group> | 6.3.5 |

**Verify-Specific Options**

| | Section |
| :--- | :--- |
| `--noscripts` Do not execute verification script | 6.3.7 |
| `--nodeps` Do not verify dependencies | 6.3.6 |
| `--nofiles` Do not verify file attributes | 6.3.8 |

**General Options**

| | Section |
| :--- | :--- |
| `-v` Display additional information | 6.3.9 |
| `-vv` Display debugging information | 6.3.10 |
| `--root <path>` Set alternate root to <path> | 6.3.12 |
| `--rcfile <rcfile>` Set alternate rpmrc file to <rcfile> | 6.3.13 |
| `--dbpath <path>` Use <path> to find the RPM database | 6.3.11 |

# ## 6.1. `rpm -V`: What Does It Do?

From time to time, it's necessary to make sure that everything on your system is okay. Are you sure the packages you've installed are still configured properly? Have there been any changes made that you don't know about? Did you mistakenly start a recursive delete in /usr and now you have to assess the damage?

RPM can help. It can alert you to changes made to any of the files installed by RPM. Also, if a package requires capabilities provided by another package, it can make sure the other package is installed, too.

The command `rpm -V` (or `-y`, or `--verify`, which are equivalent) verifies an installed package. Before we see how this is done, let's take a step back and look at the big picture.
Every time a package is installed, upgraded, or erased, the changes are logged in RPM's database. It's necessary for RPM to keep track of this information; otherwise, it wouldn't be able to perform these operations correctly. You can think of the RPM database (and the disk space it