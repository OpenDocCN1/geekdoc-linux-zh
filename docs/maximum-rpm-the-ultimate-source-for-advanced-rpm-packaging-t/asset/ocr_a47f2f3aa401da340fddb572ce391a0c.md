# ## 6.3. Selecting What to Verify and How

There are several ways to verify packages installed on your system. If you've taken a look at RPM's query command, you'll find that many of them are similar. Let's start with the simplest method of specifying packages: the package label.

# ### 6.3.1. The Package Label: Verify an Installed Package Against the RPM Database

You can simply follow the `rpm -v` command with all or part of a package label. As with every other RPM command that accepts package labels, you'll need to carefully specify each part of the label you include. Keep in mind that package names are case sensitive, so `rpm -V PackageName` and `rpm -v packagename` are not the same. Let's verify the `initscripts` package:

```
```
# rpm -v initscripts
```

```

Although it looks like RPM didn't do anything, the following steps were performed:

+   1. For every file in the package, RPM checked the nine file attributes discussed earlier.
+   2. If the package was built with dependencies, the RPM database was searched to ensure that the packages that satisfy those dependencies were installed.
+   3. If the package was built with a verification script, that script was executed.

In our example, each of these steps was performed without error\u2014the package verified successfully. Remember, with `rpm -v` you'll only see output if a package fails to verify.

# ### 6.3.2. -a: Verify All Installed Packages Against the RPM Database

If you add `-a` to `rpm -V`, you can easily verify every installed package on your system. It might take a while, but when it's done, you'll know exactly what's been changed on your system:

```
```
# rpm -Va
.M5....T   /usr/X11R6/lib/X11/fonts/misc/fonts.dir
missing    /var/spool/at/.lockfile
missing    /var/spool/at/spool
S.S....T   /usr/lib/rhs/glint/icon.pyc
..5.....T c /etc/inittab
..5.....   /usr/bin/loadkeys
```

```

Don't be too surprised if `rpm -Va` turns up a surprising number of files that failed verification. RPM's verification process is very strict! In many cases, the changes flagged don't indicate problems\u2014they are only an indication of your system's configuration being different from what