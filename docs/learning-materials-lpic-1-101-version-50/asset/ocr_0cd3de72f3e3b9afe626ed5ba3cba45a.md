effects, subpixel imaging and antialiasing, and conversions, together with multilevel undo. The GIMP offers a scripting facility, but many of the included scripts rely on fonts that we cannot distribute.

# Managing Software Repositories

zypper can also be used to manage software repositories. To see a list of all the repositories currently registered in your system, use `zypper repos`:

```
# zypper repos
Repository priorities are without effect. All enabled repositories share the same priority.
#    | Alias                  | Name                           | Enabled | GPG Check | Refresh
-------+------------------------+--------------------------------+---------+-----------+--------
   1 | openSUSE-Leap-15.1-1 | openSUSE-Leap-15.1-1           | No      | (r ) ---- | ----
   2 | repo-debug           | Debug Repository               | No      | (r ) ---- | ----
   3 | repo-debug-non-oss   | Debug Repository (Non-OSS)     | No      | (r ) ---- | ----
   4 | repo-debug-update    | Update Repository (Debug)      | No      | (r ) ---- | ----
   5 | repo-debug-update-non-oss | Update Repository (Debug, Non-OSS) | No    | (r ) ---- | ----
   6 | repo-non-oss         | Non-OSS Repository             | Yes     | (r ) Yes  | Yes
   7 | repo-oss             | Main Repository                | Yes     | (r ) Yes  | Yes
   8 | repo-source          | Source Repository              | No      | (r ) ---- | ----
   9 | repo-source-non-oss  | Source Repository (Non-OSS)    | No      | (r ) ---- | ----
  10 | repo-update          | Main Update Repository         | Yes     | (r ) Yes  | Yes
  11 | repo-update-non-oss  | Update Repository (Non-Oss)    | Yes     | (r ) Yes  | Yes
```

See in the Enabled column that some repositories are enabled, while others are not. You can change this with the `modifyrepo` operator, followed by the -e (enable) or -d (disable) parameter and the repository alias (the second column in the output above).