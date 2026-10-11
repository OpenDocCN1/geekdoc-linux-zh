However, two parts of RPM's build process are fairly constant from one package to another: the unpacking and patching of sources. RPM makes two macros available to simplify these tasks:

+   The `%setup` macro, which is used to unpack the original sources.
+   The `%patch` macro, which is used to apply patches to the original sources.

These macros are used exclusively in the `%prep` script; it wouldn't make sense to use them anywhere else. The use of these macros is not mandatory—it is certainly possible to write a `%prep` script without them. But in the vast majority of cases they make life easier for the package builder.

# 13.4.1. The %setup Macro

As mentioned earlier, the `%setup` macro is used to unpack the original sources, in preparation for the build. In its simplest form, the macro is used with no options and gets the name of the source archive from the source tag specified earlier in the spec file. Let's look at an example. The cdp layer package has the following source tag:

```
Source: ftp://ftp.gnomevision.com/pub/cdplayer/cdplayer-1.0.tgz
```

and the following `%prep` script:

```
%prep
%setup
```

In this simple case, the `%setup` macro expands into the following commands:

```
cd /usr/src/redhat/BUILD
rm -rf cdp layer-1.0
gzip -dc /usr/src/redhat/SOURCES/cdplayer-1.0.tgz | tar -xvvf -
if [ $? -ne 0 ]; then
  exit $?
fi
cd cdplayer-1.0
cd /usr/src/redhat/BUILD/cdplayer-1.0 chown -R root.root .
chmod -R a+rX,g-w,o-w .
```

As you can see, the `%setup` macro starts by changing directory into RPM's build area and removing any cdp layer build trees from previous builds. It then uses `gzip` to decompress the original source (whose name was taken from the source tag), and pipes the result to `tar` for unpacking. The return status of the unpacking is tested. If successful, the macro continues.

At this point, the original sources have been unpacked. The `%setup` macro continues by changing directory into cdp layer's top-level directory. The two `cd` commands are an artifact of `%setup`'s macro expansion. Finally, `%setup` makes sure every file in the build tree is owned by root and has appropriate permissions set.

But that's just the simplest way that `%setup` can be used. A number of other options can be added to accommodate different situations. Let's look at them.