
## 9.1.3. Patching Upstream Code (Inferred Context)

Hunk #1 succeeded at 53 (offset -1 lines).
`$ dch --local buxy "Apply patch to work with scapy 2.3"`

At this point, you have manually patched the source code and you can already build binary packages of your modified version (see section 9.1.4, “Starting the Build” [page 230]). But if you try to build an updated source package, it will fail, complaining about “unexpected upstream changes.” This is because pyrit (like a majority of the source packages) uses the source format (see `debian/source/format` file) known as 3.0 (quilt), where changes to the upstream code must be recorded in separate patches stored in `debian/patches/` and where the `debian/patches/series` file indicates the order in which patches must be applied. You can register your changes in a new patch by running `dpkg-source --commit`:

```
$ dpkg-source --commit
dpkg-source: info: local changes detected, the modified files are:
 pyrit-0.4.0/cpyrit/pckitools.py
Enter the desired patch name: fix-for-scapy-2.3.patch
dpkg-source: info: local changes have been recorded in a new patch: pyrit-0.4.0/debian/patches/fix-for-scapy-2.3.patch
$ tail -n 1 debian/patches/series
fix-for-scapy-2.3.patch
```

> **Quilt Patch Series**
> This patch management convention has been popularized by a tool named quilt and the “3.0 (quilt)” source package format is thus compatible with this tool—with the small deviation that it uses `debian/patches` instead of `patches`. This tool is available in the package of the same name and you can find a nice tutorial here:
> https://raphaeltz.co/2012/08/08/how-to-use-quilt-to-manage-patches-in-debian-packages/

If the source package uses the 1.0 or 3.0 (native) source format, then there is no requirement to register your upstream changes in a patch. They are automatically bundled in the resulting source package.

**With a Git Repository**
If you have used Git to retrieve the source package, the situation is even more complicated. There are multiple Git workflows and associated tools, and obviously not all Debian packages are using the same workflows and tools. The distinction already explained about source format is still relevant but you must also check whether patches are pre-applied in the source tree or whether they are only stored in `debian/patches` (in this case, they are then applied at build time).

The most popular tool is `git-buildpackage`. It is what we use to manage all repositories on git.kali.org. When you use it, patches are not pre-applied in the source tree but they are stored in `debian/patches`. You can manually add patches in that directory and list them in `debian/patches/series` but users of git-buildpackage tend to use `gbp pq` to edit the entire patch series as a single branch that you can extend or rebase to your liking. Check `gbp-pq(1)` to learn how to invoke it. `git-dpm` (with associated command of the same name) is another git packaging tool that you can find in use. It records metadata in `debian/.git-dpm` and keeps patches applied in the source tree by merging a constantly-rebased branch that it builds out of the content of `debian/patches`.

### 9.1.4. Tweaking Build Options

You usually have to tweak build options when you want to enable an optional feature or behavior that is not activated in the official package, or when you want to customize parameters that are set at build time through a `./configure` option or through variables set in the build environment.

In those cases, the changes are usually limited to `debian/rules`, which drives the steps in the package build process. In the simplest cases, the lines concerning the initial configuration (`./configure ...`) or the actual build (`${MAKE} ...` or `make ...`) are easy to spot. If these commands are not explicitly called, they are probably a side effect of another explicit command, in which case, please refer to their documentation to learn more about how to change the default behavior. With packages using `dh`, you might need to add an override for the `dh_auto_configure` or `dh_auto_build` commands (see their respective manual pages for explanations on how to achieve this).

To make those explanations more concrete, let's apply them to our sample use case. You decided to modify `libfreefare` to pass the `--enable-debug` option to the `./configure` script so that you could get a more verbose output from your Near field communication (NFC) tools and file a better bug report about your non-recognized Mifare NFC card. Since the package uses `dh` to drive the build process, you add (or in this case modify) the `override_dh_auto_configure` target. Here is the corresponding extract of `libfreefare`'s `debian/rules` file:

```
override_dh_auto_configure:
	dh_auto_configure -- --without-cutter --disable-silent-rules --enable-debug
```

### 9.1.5. Packaging a New Upstream Version

Let's take a look at an example at this point, as we discuss packaging upstream versions. Let's say you are a SET power-user and you noticed a new upstream release (7.4.5) that is not yet available in Kali (which only has version 7.4.4). You want to build an updated package and try it out. This is a minor version bump and you thus don't expect the update to require any change at the packaging level.

To update the source package, you extract the new source tarball next to the current source package and you copy the `debian` directory from the current source package to the new one. Then you bump the version in `debian/changelog`.

```
$ apt source set
Reading package lists... Done
NOTICE: 'set' packaging is maintained in the 'Git' version control system at:
git://git.kali.org/packages/set.git
Please use:
git clone git://git.kali.org/packages/set.git
to retrieve the latest (possibly unreleased) updates to the package.
Need to get 42.3 MB of source archives.
[...]
dpkg-source: warning: failed to verify signature on ./set_7.4.4-0kali1.dsc
dpkg-source: info: extracting set in set-7.4.4
dpkg-source: info: unpacking set_7.4.4.orig.tar.gz
dpkg-source: info: unpacking set_7.4-0kali1.debian.tar.xz
dpkg-source: info: applying edit-config-file
dpkg-source: info: applying fix-path-interpreter.patch
$ wget https://github.com/trustedsec/social-engineer-toolkit/archive/7.4.5.tar.gz -O \
            set_7.4.5.orig.tar.gz
[...]
$ tar xvf set_7.4.5.orig.tar.gz
[...]
social-engineer-toolkit-7.4.5/src/wireless/wifiattack.py
$ cp -a set-7.4.4/debian social-engineer-toolkit-7.4.5/debian
$ cd social-engineer-toolkit-7.4.5
$ dch -v 7.4.5-0buxy1 "New upstream release"
```

That’s it. You can now build the updated package.

Depending on the kind of changes that the new upstream version introduces, you may also need to change build dependencies and run-time dependencies, and install new files. Those are much more involved operations that are not covered by this book.

## 9.1.4. Starting the Build

When all the needed changes have been applied to the sources, you can start generating the actual binary package or `.deb` file. The whole process is managed by the `dpkg-buildpackage` command and it looks like this:

```
$ dpkg-buildpackage -us -uc -b
dpkg-buildpackage: source package libfreefare
dpkg-buildpackage: source version 0.4.0-0buxy1
dpkg-buildpackage: source distribution UNRELEASED
dpkg-buildpackage: source changed by Raphael Hertzog <raphael@kali.org>
dpkg-buildpackage: host architecture amd64
[...]
dh_builddeb
dpkg-deb: building package 'libfreefare0-dbg:arm' in '../libfreefare0-dbg:arm_0.4.0-0buxy1_amd64.deb'.
dpkg-deb: building package 'libfreefare0' in '../libfreefare0_0.4.0-0buxy1_amd64.deb'.
dpkg-deb: building package 'libfreefare-dev' in '../libfreefare-dev_0.4.0-0buxy1_amd64.deb'.
dpkg-deb: building package 'libfreefare-bin-dbg:arm' in '../libfreefare-bin-dbg:arm_0.4.0-0buxy1_amd64.deb'.
dpkg-deb: building package 'libfreefare-bin' in '../libfreefare-bin_0.4.0-0buxy1_amd64.deb'.
dpkg-deb: building package 'libfreefare-doc' in '../libfreefare-doc_0.4.0-0buxy1_all.deb'.
dpkg-genchanges: > .../libfreefare_0.4.0-0buxy1_amd64.changes
dpkg-genchanges: binary-only upload (no source code included)
dpkg-source --after-build libfreefare-0.4.0
dpkg-buildpackage: binary-only upload (no source included)
```

The `-us -uc` options disable signatures on some of the generated files (`.dsc`, `.changes`) because this operation will fail if you do not have a GnuPG key associated with the identity you have put in the `changelog` file. The `-b` option asks for a “binary-only build.” In this case, the source package (`.dsc`) will not be created, only the binary (`.deb`) packages will. Use this option to avoid failures during the source package build: if you haven’t properly recorded your changes in the patch management system, it might complain and interrupt the build process.

As suggested by `dpkg-deb`’s messages, the generated binary packages are now available in the parent directory (the one that hosts the directory of the source package). You can install them with `dpkg -i` or `apt install`.

```
$ sudo apt install ../libfreefare0_0.4.0-0buxy1_amd64.deb \
    ../libfreefare-bin_0.4.0-0buxy1_amd64.deb
Reading package lists... Done
Building dependency tree
Reading state information... Done
Note, selecting 'libfreefare0' instead of '../libfreefare0_0.4.0-0buxy1_amd64.deb'
Note, selecting 'libfreefare-bin' instead of '../libfreefare-bin_0.4.0-0buxy1_amd64.deb'
The following packages will be upgraded:
  libfreefare-bin libfreefare
2 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 0 B/69,4 kB of archives.
After this operation, 2048 B of additional disk space will be used.
[...]
```

We prefer `apt install` over `dpkg -i` as it will deal with missing dependencies gracefully. But not so long ago, you had to use `dpkg` as `apt` was not able to deal with `.deb` files outside of any repository.

| dpkg-buildpackage wrappers | More often than not, Debian developers use a higher-level program such as `debuild`; this runs `dpkg-buildpackage` as usual, but it also adds an invocation of a program (`lintian`) that runs many checks to validate the generated package against the Debian policy. This script also cleans up the environment so that local environment variables do not pollute the package build. The `debuild` command is one of the tools in the `devscripts` suite, which share some consistency and configuration to make the maintainers’ task easier. |
| :--- | :--- |

https://www.debian.org/doc/debian-policy/
