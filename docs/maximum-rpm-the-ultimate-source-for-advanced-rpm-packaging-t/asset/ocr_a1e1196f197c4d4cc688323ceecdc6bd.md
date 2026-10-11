Once again, there's not very much output. This is because the test succeeded; had there been a problem, the output would have been a bit more interesting. In this example, there are some problems:

```
# rpm -i --test rpm-2.0.11-1.i386.rpm
/bin/rpm conflicts with file from rpm-2.3-1
/usr/bin/gendiff conflicts with file from rpm-2.3-1
/usr/bin/rpm2cpio conflicts with file from rpm-2.3-1
/usr/bin/rpmconvert conflicts with file from rpm-2.3-1
/usr/man/man8/rpm.8 conflicts with file from rpm-2.3-1
error: rpm-2.0.11-1.i386.rpm cannot be installed
#
```

Note the version numbers. We're trying to install an older version of RPM (2.0.11) on top of a newer version (2.3). RPM faithfully reported the various file conflicts and summarized with a message saying that the install would not have proceeded, even if --test had not been on the command line.

The --test option will also catch dependency-related problems:

```
# rpm -i --test blather-7.9-1.i386.rpm
failed dependencies:
bother >= 3.1 is needed by blather-7.9-1
#
```

> TIP
> Here's a tip for all you script writers out there: RPM will return a nonzero status if the --test option detects problems.

# 2.4.3. --replacepkgs: Install the Package Even if It's Already Installed

The --replacepkgs option is used to force RPM to install a package that it believes to be installed already. This option is normally used if the installed package has been damaged somehow and needs to be fixed up.

To see how the --replacepkgs option works, let's first install some software:

```
# rpm -iv cdp-0.33-2.i386.rpm
Installing cdp-0.33-2.i386.rpm
#
```

Okay, now that we have cdp-0.33-2 installed, let's see what happens if we try to install the same version on top of itself:

```
# rpm -iv cdp-0.33-2.i386.rpm
Installing cdp-0.33-2.i386.rpm
package cdp-0.33-2 is already installed
error: cdp-0.33-2.i386.rpm cannot be installed
#
```