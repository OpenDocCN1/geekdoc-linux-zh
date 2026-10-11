Chapter 13 ▪ Inside the Spec File 185

# 13.4.1.1. -n <name>：Set Name of Build Directory

In the preceding example, the $setup macro simply uncompressed and unpacked the sources.

In this case, the tar file containing the original sources was created so that the top-level directory was included in the tar file. The name of the top-level directory was also identical to that of the tar file, which was in <name> -<version> format.

However, this is not always the case. Quite often, the original sources unpack into a directory whose name is different from the original tar file. Since RPM assumes that the directory will be called <name> -<version>, when the directory is called something else, it’s necessary to use $setup’s -n option. Here’s an example: Assume for a moment that the cdplayer sources, when unpacked, create a top-level directory named cd-player. In this case, our $setup line would look like this:

```
$setup -n cd-player
```

and the resulting commands would look like this:

```
cd /usr/src/redhat/BUILD
rm -rf cd-player
gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz | tar -xvzf -
if [ $? -ne 0 ]; then
    exit $?
fi
cd cd-player
cd /usr/src/redhat/BUILD/cd-player
chown -R root.root .
chmod -R a+rx,g-w,o-w .
```

The results are identical to using $setup with no options, except for the fact that $setup now does a recursive delete on the directory cd-player (instead of cdplayer-1.0) and changes directory into cd-player (instead of cdplayer-1.0).

Note that all subsequent build-time scripts will change directory into the directory specified by the -n option. This makes -n unsuitable as a means of unpacking sources in directories other than the top-level build directory. In the following sections, we’ll show a way around this restriction.

A quick word of warning: If the name specified with the -n option doesn’t match the name of the directory created when the sources are unpacked, the build will stop pretty quickly, so it pays to be careful when using this option.

# 13.4.1.2. -c：Create Directory (and Change to It) Before Unpacking

How many times have you grabbed a tar file and unpacked it, only to find that it is splattered files all over your current directory? Sometimes source archives are created without a top-level directory.

As you can see from the examples so far, $setup expects the archive to create its own top-level directory. If this isn’t the case, you’ll need to use the -c option.