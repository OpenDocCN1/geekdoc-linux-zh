
Hunk #1 succeeded at 53 (offset -1 lines).
$ --local doxy "Apply patch to work with scapy 2.3"

At this point, you have manually patched the source code and you can already build binary packages of your modified version (see section 9.1.4, "Starting the Build" [page 231]). But if you try to build an updated source package, you will find complaining about "unexpected upstream changes." This is because pyrit (like a majority of the source packages) uses the source debian/source-format known as 3.0 (qu), where changes to the upstream code must be recorded in separate patches stored in debian/patches/ and where the debian/patches/series file indicates the order in which patches must be applied. You can register your changes in a new patch by running dpkg-source --commit:

```
$ dpkg-source --commit
dpkg-source: info: local changes detected, the modified files are:
pyrit-0.4.0/cpyrit/pcktools.py
enter the desired patch name: fix-for-scapy-2.3.patch
dpkg-source: info: local changes have been recorded in a new patch: pyrit-0.4.0/debian/
  ► patches/fix-for-scapy-2.3.patch
  tail -n 1 debian/patches/series
fix-for-scapy-2.3.patch
```

### Quilt Patch Series
This patch management has been popularized by a tool named quilt and the "3.0 (qu)" format is compatible with this tool—with small deviation that it uses debian/patches instead of patches. This tool is available in the package with the same name and you can find a nice tutorial here:

> ► https://raphaelhertzog.com/2012/02/08/how-to-use-quit-to-manage-in-debian-packages/

If the source package uses the 1.0 or 3.0 (native) source format, then there is no requirement to register your upstream changes in a patch. They are automatically bundled in the resulting source package.

### With a Git Repository
If you used Git to retrieve the source package, the situation is even more complicated. There are multiple Git workflows and associated tools, and obviously not all Debian packages are using the same workflows and tools. The distinction already explained about source format is still relevant but you must check whether patches are pre-applied in the source tree or whether they are only stored in debian/patches (in case, they are applied at build time).

The most popular tool is git-buildpackage. It is what we use to manage all repositories on git.com/kalilinux/packages. When you use it, patches are not pre-applied in the source tree but they are stored in debian/patches. You can manually add patches in that directory and list them in debian/patches/series users of git-buildpackage tend to use gbp pq to edit the entire patch series as a single branch that you can extend or rebase to your liking. Check gbp-pq(1) to learn how to invoke it.

git-dpm (with associated command of the same name) is another git packaging tool that you can find in it. It records metadata in debian/.git-dpm and keeps patches applied in the source tree by merging a constantly-rebased branch that it builds out of the content of debian/patches.

## Tweaking Build Options

You usually have to tweak build options when you want to enable an optional feature or behavior that is not activated in the official package, or when you want to customize parameters that are set at build time through a ./configure option or variables set in the build environment.

In those cases, the changes are usually limited to debian/, which drives the steps in the package build process. In the simplest cases, the lines concerning the initial configuration (/configure ...) or the actual build (MAKE ... or make ...) are easy to spot. If these commands are not explicitly caught, they are probably a side effect of another explicit command, in which please refer to their documentation to learn more how to change the default behavior. With packages using dh, you might need to add an override for the dh_auto_configure or dh_auto_build commands (see their respective manual pages for explanations on how to achieve this).

To make these explanations more concrete, let's apply them to our sample case. You decided to modify libfreebase to pass the --enable-debug option to the ./configure script so that you get a more verbose output from your field communication (NFC) tools and find a better bug report about your non-recognized NFC card. Since the package using dh to drive the build process, you (or in this case modify) the override_dh_auto_configure target. Here is the corresponding extract of libfreebase's debian/rules file:

```
override_dh_auto_configure: --n-without-cutter --disable-silent-rules --enable-debug
  dh_auto_configure
```

## Packaging a New Upstream Version

Let's take a look at an example at this point, as we discuss packaging upstream versions. Let's say you are a SET power-user and noticed a new upstream release (7.4.5) is not yet available in Kali (which only has version 7.4.4). You want to build an updated package and try it out. This is a minor version bump and you don't expect the update to require any change at the packaging level.

To update the source package, you extract the new source tarball to the current source package and you copy the debian directory from the current source to the new one. Then you bump the version in debian/changelog.

```
$ apt source set
Reading package lists... Done
NOTICE: 'set' is maintained in the 'Git' version control system at https://gitlab.com/kalilinux/packages/set
Please use: git clone https://gitlab.com/kalilinux/packages/set.git
to retrieve the latest (possibly unreleased) updates to the package.
Need to get 2.3 MB of source archives.
dpkg-source: warning: failed to verify signature on ./set_7.4.4.dsc
dpkg-source: info: extracting set in set-7.4.4
dpkg-source: info: unpacking set-7.4.4.orig.gz
dpkg-source: info: unpacking set-7.4.4.xz
dpkg-source: info: applying config
$ wget https://github.com/trusted/social-engineer-toolkit/archive/7.4.5.tar.gz -O set_7.4.5.tar.gz
$ tar xvf set_7.4.5.tar.gz social-engineer-toolkit/set-7.4.5/src/wireless/attack.py
$ cp -a set-7.4.4/debian social-engineer-toolkit/set-7.4.5/debian
$ cd social-engineer-toolkit/set-7.4.5
$ dch -v 7.4.5-1 "New upstream release"
```

That's how you can now build the updated package. Depending on the kind of changes that the upstream version introduces, you may also need to change build and run-time dependencies, and install new files.

## 9.1.4 Starting the Build

When all the changes have been applied to the sources, you can start generating the actual binary package or .deb file. The whole process is managed by the dpkg-buildpackage command and it looks like:

```
$ dpkg-buildpackage -us -b
dpkg-package: source package libfree
dpkg-package: source version 0.4.0-1
dpkg-package: distribution RELEASE
dpkg-package: created by Raphael Hertzog <raphael@kali.org>
dpkg-package: host architecture amd64
debuild
dpkg-deb: building package 'libfree-dbgsym' in .../libfree-dbgsym_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree' in .../libfree_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree-dev' in .../libfree-dev_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree-bin-dbgsym' in .../libfree-bin-dbgsym_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree-bin' in .../libfree-bin_0.4.0-1.amd64.deb
dpkg-deb: building package 'libfree-doc' in .../libfree-doc_0.4.0-1.all.deb
dpkg-changes -b ./libfree-doc_0.4.0-1.all.deb
dpkg-changes: binary-only upload (no source included)
dpkg-source -after-build libfree-0.4.0-1
dpkg-package: binary-only upload (no source included)
```

The -uc options silence signatures on some of the generated files (.dsc), because operation will fail if you do not have a GNU key with the identity you have put in the changelog file. The -b option asks for a 'binary-only build'. In this, the source package (.dsc) will not be created, only the binary (.deb) packages will. Use this to avoid failures during the source package build: if you haven't properly recorded your changes in the patch management system, it might complain and interrupt the build process.

As suggested by dpkg-dev messages, the generated binary packages are now available in the parent directory (the one above the source package). You can install them with dpkg-i or apt install.

```
$ sudo apt install ../libfree_0.4.0-1.amd64.deb \
../libfree-bin_0.4.0-1.amd64.deb
```

Reading package lists... Done
Building dependency tree
Reading state information... Done
Note, selecting 'libfree' instead of '../libfree0_0.4.0-1.amd64.deb'
Note, selecting 'libfree-bin' instead of './libfree-bin_0.4.0-1.amd64.deb'
The following packages will be upgraded:
libfree libfree0
2 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need 0 B/69.4 KB of archives.
After this operation, 2048 B of additional disk space will be used.

We prefer apt install dpkg -i as it will deal with the generated files gracefully. But not so long ago, you had to use dpkg as not able to deal with .deb files outside of any repository.

| dpkg-buildpackage wrappers | More than not, Debian developers use a higher-level program as debbuild; this runs dpkg-buildpackage as usual, but it also adds an invocation of a program (Lintian) that runs many times to validate the generated package against the Debian policy. This script cleans up the environment so local environment variables do not pollute the package build. The default command is one of the tools in the devsucripts, which share some consistency and configuration to make the maintainers' task easier. |

> ³https://www.debian.org/doc/debian-policy/
