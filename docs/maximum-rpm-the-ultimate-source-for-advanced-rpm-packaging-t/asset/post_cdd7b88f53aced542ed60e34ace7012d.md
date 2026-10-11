
RPM has another tag that can be used with the `--queryformat` option. It’s called `INSTALLPREFIX`, and using it displays the prefix under which a package was installed. Let’s give it a try:

```bash
# rpm -q --queryformat '%{INSTALLPREFIX}\n' cdplayer
/usr/foonly/blather
#
```

As you can see, it displays the prefix you entered on the command line. Let’s see if the files were installed as directed:

```bash
# cd /usr/foonly/blather/
# ls -al
total 2
drwxr-xr-x 2 root root 1024 Oct 7 13:45 bin/
drwxr-xr-x 3 root root 1024 Oct 7 13:45 man/
#
```

So far, so good—the proper directories are there. Let’s look at the man page first:

```bash
# cd /usr/foonly/blather/man/man1/
# ls -al
total 5
-rwxr-xr-x 1 root root 4550 Oct 7 13:23 cdp.1*
#
```

That looks okay. Now on to the files in bin:

```bash
# cd /usr/foonly/blather/bin
# ls -al
total 41
-rwxr-xr-x 1 root root 40739 Oct 7 13:23 cdp*
lrwxrwxrwx 1 root root 18 Oct 7 13:45 cdplay -> /usr/local/bin/cdp
```

Uh-oh. That `cdplay` symlink isn’t right. What happened? If we look at `cdplay`’s makefile, we see the answer:

```makefile
install: cdp cdp.1.Z
... 
ln -s /usr/local/bin/cdp /usr/local/bin/cdplay
```

Ah, when the software is installed during `RPM`’s build process, the makefile sets up the symbolic link. Looking back at the `%files` list, we see `cdplay` listed. `RPM` blindly packaged the symlink, complete with its nonrelocatable string. This is why we mentioned absolute symlinks as a prime example of nonrelocatable software.

Fortunately, this problem isn’t that difficult to fix. All we need to do is change the line in the makefile that creates the symlink from this:

```makefile
ln -s /usr/local/bin/cdp /usr/local/bin/cdplay
```

to this:

```makefile
ln -s ./cdp /usr/local/bin/cdplay
```

Now `cdplay` will always point to `cdp`, no matter where it’s installed. When building relocatable packages, relative symlinks are your friend!

After rebuilding the package, let’s see if our modifications have the desired effect. First, a normal install with the default prefix:

```bash
# rpm -Uvh --nodeps cdplayer-1.0-1.i386.rpm
cdplayer #############################################
# cd /usr/local/bin/
# ls -al cdplay
lrwxrwxrwx 1 root root 18 Oct 8 22:32 cdplay -> ./cdp*
```

Next, we’ll try a second install using the `--prefix` option (after we first delete the original package):

```bash
# rpm -e cdplayer
# rpm -Uvh --nodeps --prefix /a/dumb/prefix cdplayer-1.0-1.i386.rpm
cdplayer #############################################
# cd /a/dumb/prefix/bin/
# ls -al cdplay
lrwxrwxrwx 1 root root 30 Oct 8 22:34 cdplay -> ./cdp*
# 
```

As you can see, the trickiest part about building relocatable packages is making sure the software you’re packaging is up to the task. Once that part of the job is done, the actual modifications are straightforward.

## 16. Making a Package That Can Build Anywhere

Although RPM makes building packages as easy as possible, some of the default design decisions might not work well in a particular situation. Here are two situations where RPM’s method of package building may cause problems:

- You are unable to dedicate a system to RPM package building, or the software you’re packaging would disrupt the build system’s operation if it were installed.
- You would like to package software, but you don’t have root access to an appropriate build system.

Either of these situations can be resolved by directing RPM to build, install, and package the software in a different area on your build system. It requires a bit of additional effort to accomplish this, but taken a step at a time, it is not difficult. Basically, the process can be summed up by addressing the following steps:

- Writing the package’s spec file to support a build root
- Directing RPM to build software in a user-specified build area
- Specifying file attributes that RPM needs to set on installation

The methods discussed here are not required in every situation. For example, a system administrator developing a package on a production system may only need to add support for a build root. On the other hand, a student wishing to build a package on a university system will need to get around the lack of root access by implementing every method described here.

### 16.1. Using Build Roots in a Package

Part of the process of packaging software with RPM is to actually build the software and install it on the build system. The installation of software can be accomplished only by someone with root access, so a nonprivileged user will certainly need to handle RPM’s installation phase differently. There are times, however, when even a person with root access will not want RPM to copy new files into the system’s directories. As mentioned earlier, the reason might be due to the fact that the software being packaged is already in use on the build system. Another reason might be as mundane as not having enough free space available to perform the install into the default directories.

Whatever the reason, RPM provides the capability to direct a given package to install into an alternate root. This alternate root is known as a *build root*. Several requirements must be met in order for a build root to be utilized:

- A default build root must be defined in the package’s spec file.
- The installation method used by the software being packaged must be able to support installation in an alternate root.

The first part is easy. It entails adding the following line to the spec file:

```spec
BuildRoot: <root>
```

Of course, you would replace `<root>` with the name of the directory in which you'd like the software to install. (Keep in mind that the build root can be overridden at build time using the `--buildroot` option or the `buildroot` `rpmrc` file entry. See Chapter 12, "rpmb -b Command Reference," for more details.) If, for example, you specify a build root of `/tmp/foo`, and the software you're packaging installs a file `bar` in `/usr/bin`, you'll find `bar` residing in `/tmp/foo/usr/bin` after the build.

A note for your nonroot package builders: Make sure you can actually write to the build root you specify! Those of you with root access should also make sure you choose your build root carefully. For a variety of reasons, it's not a good idea to declare a build root of `/`. We'll get into the reasons shortly.

The final requirement for adding build root support is to make sure the software's installation method can support installing into an alternate root. The difficulty in meeting this requirement can range from dead simple to nearly impossible. There are probably as many different ways of approaching this as there are packages to build. But in general, some variant of the following approach is used:

- The environment variable **`RPM_BUILD_ROOT`** is set by RPM and contains the value of the build root to be used when the software is built and installed.
- The `%install` section of the spec file is modified to use **`RPM_BUILD_ROOT`** as part of the installation process.
- If the software is installed using **`make`**, the makefile is modified to use **`RPM_BUILD_ROOT`** and to create any directories that may not exist at installation time.

Here's an example of how these components work together to utilize a build root. First, there's the definition of the build root in the spec file:

```spec
BuildRoot: /tmp/cdplayer
```

This line defines the build root as being `/tmp/cdplayer`. All the files installed by this software will be placed under the `cdplayer` directory. Next is the spec file's `%install` section:

```spec
%install
make ROOT="$RPM_BUILD_ROOT" install
```

Since the software we're packaging uses `make` to perform the actual install, we simply define the environment variable `ROOT` to be the path defined by **`RPM_BUILD_ROOT`**. So far, so good. Things really start to get interesting in the software's makefile, though:

```makefile
install: cdp cdp.1.Z
	# chmod 755 cdp
	# cp cdp /usr/local/bin
	install -m 755 -o 0 -g 0 -d $(ROOT)/usr/local/bin/
	install -m 755 -o 0 -g 0 -d $(ROOT)/usr/local/bin/cdp
	# ln -s /usr/local/bin/cdp /usr/local/bin/cdplay
	ln -s ./cdp $(ROOT)/usr/local/bin/cdplay
	# cp cdp.1 /usr/local/man/man1
	install -m 755 -o 0 -g 0 -d $(ROOT)/usr/local/man/man1/
	install -m 755 -o 0 -g 0 -d $(ROOT)/usr/local/man/man1/cdp.1
```
