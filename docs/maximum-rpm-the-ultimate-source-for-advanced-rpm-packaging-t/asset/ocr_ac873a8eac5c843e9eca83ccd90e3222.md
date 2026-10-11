```
RPM_PACKAGE_VERSION="1.0"
RPM_PACKAGE_RELEASE="1"
set -x

umask 022
echo Executing: %prep
cd /usr/src/redhat/BUILD

cd /usr/src/redhat/BUILD
rm -rf cdplayer-1.0
gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz | tar -xvvf -
if [ $? -ne 0 ]; then
    exit $?
fi
cd cdplayer-1.0
cd /usr/src/redhat/BUILD/cdplayer-1.0
chown -R root.root .
chmod -R a+R,X,g-w,o-w .
```

As you can see, this script contains the %prep section from the spec file. The script starts by defining a number of environment variables and then leads into the %prep section. In the spec file used in this build, the %prep section consists of a single %setup macro. In this file, we can see exactly how RPM expands that macro. The remaining files follow the same basic layout— a section-defining environment variables, followed by the commands to be executed.

Note that the --test option will only create script files for each build stage, as specified in the command line. For example, if the previous command were changed to

```
# rpm -bp --test cdplayer-1.0.spec
#
```

only one script file, containing the %prep commands, would be written. In any case, no matter what RPM build command is used, the --test option can let you see exactly what is going to happen during a build.

# 12.1.12. --clean: Clean Up After Build

The --clean option can be used to ensure that the package’s build directory tree is removed at the end of a build. Although it can be used with any build stage, it doesn’t always make much sense to do so:

```
# rpm -bp --clean cdplayer-1.0.spec
* Package: cdplayer
Executing: %prep
...
+ exit 0
+ echo Executing: sweep
Executing: sweep
+ cd /usr/src/redhat/BUILD
+ rm -rf cdplayer-1.0
+ exit 0
#
```