# 15.3.1. %files List Restrictions

As mentioned earlier, each file in the `%files` list must start with the relocation prefix. If this isn’t done, the build will fail:

```
# rpm -ba cdplayer-1.0.spec
* Package: cdplayer
+ umask 022
+ echo Executing: %prep
***
Binary Packaging: cdplayer-1.0-1
Package Prefix = usr/local
File doesn’t match prefix (usr/local): /usr/doc/cdplayer-1.0-1
File not found: /usr/doc/cdplayer-1.0-1
Build failed.
```

In our example, the build proceeded normally until the time came to create the binary package file. At that point RPM detected the problem. The error message says it all: The prefix line in the spec file (usr/local) was not present in the first part of the file’s path (/usr/doc/cdplayer-1.0-1). This stopped the build in its tracks.

The fact that every file in a relocatable package must be installed under the directory specified in the prefix line raises some issues. For example, what about a program that reads a configuration file normally kept in /etc? This question leads right into our next section.

# 15.3.2. Relocatable Packages Must Contain Relocatable Software

While this section’s title seems pretty obvious, it’s not always easy to tell if a particular piece of software can be relocated. Let’s take a look at the question raised at the end of the previous section. If a program has been written to read its configuration file from /etc, there are three possible approaches to making that program relocatable:

+   - Set the prefix to /etc and package everything under /etc.
+   - Package everything somewhere other than /etc and leave out the config file entirely.
+   - Modify the program.

The first approach would certainly work from a purely technical standpoint, but not many people would be happy with a program that installed itself in /etc. So this approach isn’t viable.

The second approach might be more appropriate, but it forces users to complete the install by having them create the config file themselves. If RPM’s goal is to make software easier to install and remove, this is not a viable approach either!

The final approach might be the best. Once the program is installed, when the rewritten software is first run, it can see that no configuration file exists in /etc and create one. However, even though this would work, when the time came to erase the package, the config file would be left behind. RPM had never installed it, so RPM couldn’t get rid of it. There’s also the fact that this approach is probably more labor intensive than most package builders would like.