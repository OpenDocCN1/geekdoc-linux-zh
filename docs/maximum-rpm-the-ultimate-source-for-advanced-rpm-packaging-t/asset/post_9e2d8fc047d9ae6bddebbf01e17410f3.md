
## 15.3.3. The Relocatable Software Is Referenced by Other Software

None of these approaches are very appealing, are they? Some software just doesn't relocate very well. In general, the following things are warning signs that relocation is going to be a problem:

- The software contains one or more files that must be installed in specific directories.
- The software refers to system files using relative paths (which is really just another way of saying that the software must be installed in a particular directory).

If these kinds of issues crop up, making the software relocatable is going to be tough.

Even assuming that the software is written so that it can be put in a relocatable package, there still might be a problem, which relates not to the relocatable software itself, but to other programs that reference the relocatable software.

For example, there are times when a package needs to execute other programs. This might include backup software that needs to send mail, or a communications program that needs to compress files. If these underlying programs were relocatable, and not installed where other packages expect them, they would be of little use.

Granted, this isn't a common problem, but it can happen. And for the package builder interested in building relocatable packages, it's an issue that needs to be explored. Unfortunately, this type of problem can be the hardest to find.

If, however, a software product has been found to be relocatable, the mechanics of actually building a relocatable package are pretty straightforward. Let's give it a try.

## 15.4. Building a Relocatable Package

For this example, we'll use our tried-and-true cdp1ayer application. Let's start by reviewing the spec file for possible problems:

```
""#
# Sample spec file for cdp1ayer app...
#
Summary: A CD player app that rocks!
Name: cdp1ayer
...
%files
%doc README
/usr/local/bin/cdp
/usr/local/bin/cdplay
%doc /usr/local/man/man1/cdp.1
%config /etc/cdp-config"
```

Everything looks all right, except for the `%files` list. There are files in `/usr/local/bin`, a man page in `/usr/local/man/man1`, and a config file in `/etc`. The prefix `/usr/local` would work pretty well, except for that `cdp-config` file.

For the sake of this first build, we’ll declare the config file unnecessary and remove it from the `%files` list. We’ll then add a prefix tag line, setting the prefix to `/usr/local`. After these changes are made, let’s try a build:

```
# rpm -ba cdplayer-1.0.spec
\* Package: cdplayer
\+ umask 022
\+ echo Executing: %prep
Executing: %prep
\+ cd /usr/src/redhat/BUILD
\+ cd /usr/src/redhat/BUILD
\+ rm -rf cdplayer-1.0
\+ gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz
....
Binary Packaging: cdplayer-1.0-1
Package Prefix = usr/local
File doesn’t match prefix (usr/local): /usr/doc/cdplayer-1.0-1
File not found: /usr/doc/cdplayer-1.0-1
Build failed.
```

The build proceeded normally up to the point of actually creating the binary package. The `Package Prefix = usr/local` line confirms that RPM picked up our prefix tag line. But the build stopped—and on a file called `/usr/doc/cdplayer-1.0-1`. But that file isn’t even in the `%files` list. What’s going on?

Take a closer look at the `%files` list. See the line that reads `%doc README?` In Section 13.6.1 in Chapter 13, “Inside the Spec File,” we discussed how the `%doc` directive creates a directory under `/usr/doc`. That’s the file that killed the build—the directory created by the `%doc` directive.

Let’s temporarily remove that line from the `%files` list and try again:

```
# rpm -ba cdplayer-1.0.spec
\* Package: cdplayer
\+ umask 022
\+ echo Executing: %prep
Executing: %prep
\+ cd /usr/src/redhat/BUILD
\+ cd /usr/src/redhat/BUILD
\+ rm -rf cdplayer-1.0
\+ gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz
....
Binary Packaging: cdplayer-1.0-1
Package Prefix = usr/local
Finding dependencies...
Requires (2): libc.so.5 libncurses.so.2.0
bin/cdp
bin/cdplay
man/man1/cdp.1
90 blocks
Generating signature: 0
Wrote: /usr/src/redhat/RPMS/i386/cdplayer-1.0-1.i386.rpm
\+ umask 022
\+ echo Executing: %clean
Executing: %clean

+ cd /usr/src/redhat/BUILD

+ cd cdplayer-1.0

+ exit 0

Source Packaging: cdplayer-1.0-1

cdplayer-1.0.spec

cdplayer-1.0.tgz

82 blocks

Generating signature: 0

Wrote: /usr/src/redhat/RPMS/i/cdplayer-1.0-1.src.rpm
```

The build completed normally. Note how the files to be placed in the binary package file are listed, minus the prefix /usr/local. Some of you might be wondering why the cdp.1 file didn't cause problems. After all, it had a %doc directive, too. The answer lies in the way the file was specified. Since the file was specified using an absolute path, and that path started with the prefix /usr/local, there was no problem. A more complete discussion of the %doc directive can be found in section 13.6.1 in Chapter 13.

### 15.4.1. Tying Up the Loose Ends

In the course of building this package, we ran into two hitches:

- The config file cdp-config couldn't be installed in /etc.
- The README file could not be packaged using the %doc directive.

Both of these issues are due to the fact that the files' paths do not start with the default prefix path /usr/local. Does this mean that this package cannot be relocated? Possibly, but there are two options to consider. The first option is to review the prefix. For our example, if we chose the prefix /usr instead of /usr/local, the README file could be packaged using the %doc directive since the default documentation directory is /usr/doc. Another approach would be to use the %docdir directive to define another documentation-holding directory somewhere along the prefix path. (For more information on the %docdir directive, see section 13.6.2 in Chapter 13.)

This approach wouldn't work for /etc/cdp-config, though. To package that file, we'd need to resort to more extreme measures. Basically, this approach would entail packaging the file in an acceptable directory (something under /usr/local) and using the %post postinstall script to move the file to /etc. Pointing a symlink at the config file is another possibility.

Of course, this approach has some problems. First, you'll need to write a %postun script to undo what the %post script does. (Install and erase-time scripts have an environment variable, **RPM_INSTALL_PREFIX**, that can be used to write scripts that are able to act appropriately if the package is relocated. See section 13.3.2 in Chapter 13 for more information.) A verification script that made sure the files were in place would be nice, too. Second, because the file or symlink wasn't installed by RPM, there's no entry for it in the RPM database. This reduces the utility of `RPM`'s `-c` and `-o` options when issuing queries. Finally, if you actually move files around using the %post script, the files you move will not verify properly, and when the package is erased, your users will get some disconcerting messages when RPM can't find the moved files to erase them. If you have to resort to these kinds of tricks, it's probably best to forget trying to make the package relocatable.

## 15.4.2. Test-Driving a Relocatable Package

Looks like cdplayer is a poor candidate for being made relocatable. However, since we did get a hamstrung version to build successfully, we can use it to show how to test a relocatable package. First, let's see if the binary package file's prefix has been recorded properly. We can do this by using the --queryformat option to RPM's query mode:

```
# rpm -q --queryformat '%{DEFAULTPREFIX}\n' cdplayer-1.0-1.i386.rpm
/usr/local
#
```

The **DEFAULTPREFIX** tag directs RPM to display the prefix used during the build. As we can see, it's /usr/local, just as we intended. The --queryformat option is discussed in section 5.2.2 of Chapter 5, "Getting Information About Packages."

So it looks like we have a relocatable package. Let's try a couple installs and see if we really can install it in different locations. First, let's try a regular install with no prefix specified:

```
# rpm -Uvh cdplayer-1.0-1.i386.rpm
cdplayer ################################################################
#
```

That seemed to work well enough. Let's see if the files went where we intended:

```
# ls -a1 /usr/local/bin
total 558
-rwxr-xr-x 1 root root 40739 Oct 7 13:23 cd*
lrwxrwxrwx 1 root root 18 Oct 7 13:40 cdplay -> /usr/local/bin/cdp*
...
# ls -a1 /usr/local/man/man1
total 9
-rwxr-xr-x 1 root root 4550 Oct 7 13:23 cdpl.1*
...
#
```

Looks good. Let's erase the package and reinstall it with a different prefix:

```
# rpm -e cdplayer
# rpm -Uvh --prefix /usr/foonly/blather cdplayer-1.0-1.i386.rpm
cdplayer ################################################################
#
```

Note that directories foonly and blather didn't exist prior to installing cdplayer.
