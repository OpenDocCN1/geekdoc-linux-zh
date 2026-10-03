◆ The patch being installed requires another patch that is not installed.

# Removing a Patch

Sometimes, a patch does not work as planned and needs to be removed from the system. The utility used to remove, or “back out of,” a patch is the patchrm command, described in Table 4.5. Its syntax is as follows:

```
patchrm [ -f ] [ -B backout_dir ]
```

# TABLE 4.5

# patchrm Command Options

| Common Options | Description |
|---|---|
| -f | Forces the patch removal, regardless of whether the patch was superseded by another patch. |
| -B backout_dir | Removes a patch whose backout data has been saved to a directory other than the package database. This option is needed only if the original backout directory, supplied to the patchadd command at installation time, has been moved. Specify backout_dir as an absolute pathname. |

The following example removes a patch from a stand-alone system:

```
patchrm 104945-02
```

The patchrm command removes a Solaris 8 patch package, and restores previously saved files, restoring the file system to its state before a patch was applied, unless any of the following four conditions exist:

◆ The patch was installed with patchadd -d. (The -d option