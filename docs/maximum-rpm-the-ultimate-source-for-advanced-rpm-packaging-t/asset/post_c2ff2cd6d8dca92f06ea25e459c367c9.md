
...the builders of the installed packages had on their systems. Also, some attributes change during normal system operation. It would be wise to check into each verification failure, just to make sure.

### 6.3.3. -f <file>: Verify the Package Owning <file> Against the RPM Database

Imagine this: You’re hard at work when a program you’ve used a million times before suddenly stops working. What do you do? Well, before using RPM, you probably tried to find other files associated with that program and see if they had changed recently.

Now you can let RPM do at least part of that sleuthing for you. Simply direct RPM to verify the package owning the ailing program:

```
% rpm -Vf /sbin/cardmgr
S.5....T c /etc/sysconfig/pccmca
%
```

Hmmm. Looks like a config file was recently changed.

This isn’t to say that using RPM to verify a package will always get you out of trouble, but it’s such a quick step that it should be one of the first things you try. Here’s an example of rpm -Vf not working out as well:

```
% rpm -Vf /etc/blunder
file /etc/blunder is not owned by any package
%
```

Note that the issue surrounding RPM and symbolic links mentioned in Chapter 5, “Getting Information About Packages,” also applies to rpm -Vf. Watch those symlinks!

### 6.3.4. -p <file>: Verify Against a Specific Package File

Unlike the previous options to rpm -v, each of which verifies one or more packages against RPM’s database, the -p option performs the same verification, but against a package file. Why on earth would you want to do this when the RPM database is sitting there, just waiting to be used?

Well, what if you didn’t have an RPM database? While it isn’t a common occurrence, power failures, hardware problems, and inadvertent deletions (along with nonexistent backups) can leave your system sans database. Then your system hicups; what do you do now?

This is where a CD full of package files can be worth its weight in gold. Simply mount the CD and verify to your heart’s content:

```
# rpm -Vp /mnt/cdrom/RedHat/RPMS/i386/adaudser-1.1.1.i386.rpm
#
```

Whatever else might be wrong with this system, at least we can add new users. But what if you have many packages to verify? It would be a very slow process doing it one package at a time. That's where the next option comes in handy.

### 6.3.5. `-g <group>`: Verify Packages Belonging to `<group>`

When a package is built, the package builder must classify the package, grouping it with other packages that perform similar functions. RPM gives you the ability to verify installed packages based on their groups. For example, there is a group known as `shells`. This group consists of packages that contain, strangely enough, shells. Let's verify the proper installation of every shell-related package on the system:

```
# rpm -Vg Shells
missing /etc/bashrc
#
```

One thing to keep in mind is that group specifications are case sensitive. Issuing the command `rpm -Vg shells` wouldn't verify many packages:

```
# rpm -Vg shells
group shells does not contain any packages
#
```

### 6.3.6. `--nodeps`: Do Not Check Dependencies Before Erasing Package

When the `--nodeps` option is added to a verify command, RPM will bypass its dependency verification processing. In this example, we've added the `-vv` option to the command line so we can watch RPM at work:

```
# rpm -Vvv rpm
D: opening database in /var/lib/rpm/
D: verifying record number 2341208
D: dependencies: looking for libz.so.1
D: dependencies: looking for libdb.so.2
D: dependencies: looking for libc.so.5
#
```

As you can see, the rpm package provides three different capabilities:

- `libz.so.1`
- `libdb.so.2`
- `libc.so.5`

If we add the `--nodeps` option, the dependency verification of the three capabilities is no longer performed:

```
# rpm -Vvv --nodeps rpm
D: opening database in /var/lib/rpm/
D: verifying record number 2341208
#
```

The line D: verifying record number 2341288 indicates that RPM’s normal file-based verification proceeded normally.

### 6.3.7. --noscripts: Do Not Execute Verification Script

Adding the --noscripts option to a verify command prevents execution of the verification scripts of each package being verified. In the following example, the package verification script is executed:

```
# rpm -Vvv bother
D: opening database in ///var/lib/rpm/
D: verifying record number 616728
D: verify script found - running from file /var/tmp/rpm-321.vscript
+ PATH=/sbin:/bin:/usr/sbin:/usr/bin:/usr/X11R6/bin
+ export PATH
+ echo This is the bothe r 3.5 verification script
This is the bother 3.5 verification script
#
```

While the actual script is not very interesting, it did execute when the package was being verified. In the next example, we’ll use the --noscripts option to prevent its execution:

```
# rpm -Vvv --noscripts bother
D: opening database in ///var/lib/rpm/
D: verifying record number 616728
#
```

As expected, the output is identical to the prior example, minus the lines dealing with the verification script, of course.

### 6.3.8. --noifiles: Do Not Verify File Attributes

The --noifiles option disables RPM’s file-related verification processing. When this option is used, only the verification script and dependency verification processing are performed. In this example, the package has a file-related verification problem:

```
# rpm -Vvv bash
D: opening database in ///var/lib/rpm/
D: verifying record number 279448
D: dependencies: looking for lib.c.so.5
D: dependencies: looking for libtermcap.so.2
missing /etc/bashrc
#
```

When the --noifiles option is added, the missing file doesn’t cause a message anymore:

```
# rpm -Vvv --noifiles bash
D: opening database in ///var/lib/rpm/
D: verifying record number 279448
D: dependencies: looking for lib.c.so.5
D: dependencies: looking for libtermcap.so.2
#
```

This is not to say that the missing file problem is solved, just that no file verification was performed.

### 6.3.9. -v: Display Additional Information

Although RPM won’t report an error with the command syntax if you include the -v option, you won’t see much in the way of additional output:

```
# rpm -Vv bash
#
```

Even if there are verification errors, adding -v won’t change the output:

```
# rpm -Vv apmd
S.5....T /etc/rc.d/init.d/apmd
S.5....T /usr/X11R6/bin/xapmd
#
```

The only time that the -v option will produce output is when the package being verified has a verification script. Any normal output from the script won’t be displayed by RPM when run without -v (note that failure messages will always be displayed):

```
# rpm -V bother
#
```

But when -v is added, the script’s non-error-related output is displayed:

```
# rpm -Vv bother
This is the bother 3.5 verification script
#
```

### 6.3.10. -vv: Display Debugging Information

Sometimes it’s necessary to have even more information than we can get with -v. By adding another v, that’s just what we’ll get:

```
# rpm -Vvv rpm
D: opening database in /var/lib/rpm/
D: verifying record number 2341208
D: dependencies: looking for libz.so.1
D: dependencies: looking for libdb.so.2
D: dependencies: looking for libc.so.5
#
```

The lines starting with D: have been added by using -vv. We can see where the RPM database is located and what record number contains information on the rpm-2.3-1 package. Following that is the list of dependencies that the rpm package requires.

In the vast majority of cases, it will not be necessary to use -vv. It is normally used by software engineers working on RPM itself, and the output can change without notice. However, it’s a handy way to gain insights into RPM.

### 6.3.11. --dbpath <path>: Use <path> to Find an RPM Database

In order for RPM to do its handiwork, it needs access to an RPM database. Normally, this database exists in the directory specified by the rpmlrc file entry, dbpath. By default, dbpath is set to /var/lib/rpm. Although the dbpath entry can be modified in the appropriate rpmlrc file, the --dbpath option is probably a better choice when the database path needs to be changed temporarily. An example of a time the --dbpath option would come in handy is when it's necessary to examine an RPM database copied from another system. Granted, it's not a common occurrence, but it's difficult to handle any other way.

### 6.3.12. --root <path>: Set Alternate Root to <path>

Adding --root <path> to a verify command forces RPM to assume that the directory specified by <path> is actually the root directory. In addition, RPM expects its database to reside in the directory specified by the dbpath rpmlrc file entry, relative to <path>. (For more information on rpmlrc file entries, see Appendix B, "The rpmlrc File.")

Normally this option is only used during an initial system install or when a system has been booted off a rescue disk.

### 6.3.13. --rcfile <rcfile>: Set Alternate rpmlrc File to <rcfile>

The --rcfile option is used to specify a file containing default settings for RPM. Normally, this option is not needed. By default, RPM uses /etc/rpmrc and a file named .rpmlrc, located in your login directory.

This option would be used if there were a need to switch between several sets of RPM options. Software developer and package builders will be the people using --rcfile. For more information on rpmlrc files, see Appendix B.

## 6.4. We've Lied to You

Not really; we just omitted a few details until you've had a chance to see rpm -v in action. These details are described in the following sections.

### 6.4.1. RPM Controls What Gets Verified

Depending on the type of file being verified, RPM will not verify every possible attribute. Table 6.2 shows the attributes checked for each of the different file types.
