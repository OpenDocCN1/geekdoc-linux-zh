in debian/patches/series users of git-buildpackage tend to use gbp pq to edit the entire patch series as a single branch that you can extend or rebase to your liking. Check gbp-pq(1) to learn how to invoke it.

git-dpm (with associated command of the same name) is another git packaging tool that you can find in it. It records metadata in debian/.git-dpm and keeps patches applied in the source tree by merging a constantly-rebased branch that it builds out of the content of debian/patches.

# Tweaking Build Options

You usually have to tweak build options when you want to enable an optional feature or behavior that is not activated in the official package, or when you want to customize parameters that are set at build time through a ./configure option or variables set in the build environment.

In those cases, the changes are usually limited to debian/, which drives the steps in the package build process. In the simplest cases, the lines concerning the initial configuration (/configure ...) or the actual build (MAKE ... or make ...) are easy to spot. If these commands are not explicitly caught, they are probably a side effect of another explicit command, in which please refer to their documentation to learn more about how to change the default behavior. With packages using dh, you might need to add an override for the dh_auto_configure or dh_auto_build commands (see their respective manual pages for explanations on how to achieve this).

To make these explanations more concrete, let's apply them to our sample case. You decided to modify libfreebase to pass the --enable-debug option to the ./configure script so that you get a more verbose output from your field communication (NFC) tools and find a better bug report about your non-recognized NFC card. Since the package using dh to drive the build process, you (or in this case modify) the override_dh_auto_configure target. Here is the corresponding extract of libfreebase's debian/rules file:

```
override_dh_auto_configure: --n-without-cutter --disable-silent-rules --enable-debug
  dh_auto_configure
```

# Packaging a New Upstream Version

Let's take a look at an example at this point, as we discuss packaging upstream versions. Let's say you are a SET power-user and noticed a new upstream release (7.4.5) is not yet available in Kali (which only has version 7.4.4). You want to build an updated package and try it out. This is a minor version bump and you don't expect the update to require any change at the packaging level.