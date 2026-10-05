a editor (sensible-editor, which runs the editor assigned in the VISUAL or EDITOR environment variables, or /usr/bin/editor otherwise), which allows you to document the differences introduced by this rebuild. This editor shows that dch really did change debian/changelog file:

```
$ head -n 1 debian/changelog
libfreere (0.4.0-2) unstable; urgency=low
$ dch --local buxy
[...
$ head debian/changelog
libfreere (0.4.0-2-buxy1) UNRELEASED; urgency=medium
```

+   * Enable --with-debug configure option.
* Raphael Hertzog <bxy@kali.org> -- Fri, 22 Apr 2016 10:36:00 -04400

libfreere (0.4.0-2) unstable; urgency=low

+   * Update debian/copyright.
Fix license to LGPL3+.

If you do such changes regularly

# Applying a Patch

In one of our cases, we have downloaded the pyrit source package and we want to apply a patch that we found in the upstream git repository. This is a common operation and it should always be simple. Unfortunately, patches can be handled in different ways depending on the source package format and on the Git packaging workflow in (when Git is used to maintain the package).

**With an Unpacked Source Package** run apt source pyrit and you have a pyrit-0. 4.0 directory. You can apply your patch directly with patch -p1 < patch-file:

```
$ apt source pyrit
[...
$ cd pyrit-0.4.0
$ wget https://github.com/JPaulMora/pyrit/commit/14
→ ec99174b8e8fd2022b6a97c57e19633f12a0-0 /tmp/pyrit-patch
[...]
$ patch -p1 </tmp/pyrit-patch
patching file cpyrt/pcktools.py
```