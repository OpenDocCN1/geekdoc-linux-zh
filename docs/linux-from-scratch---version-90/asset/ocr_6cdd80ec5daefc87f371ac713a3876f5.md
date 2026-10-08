# #64. Kbd-2.2.0

The Kbd package contains key-table files, console fonts, and keyboard utilities.
Approximate build time: 0.2 SBU
Required disk space: 36 MB

# ## 64.1. Installation of Kbd

The behaviour of the Backspace and Delete keys is not consistent across the keymaps in the Kbd package. The following patch fixes this issue for i386 keyboards:

```
patch -Np1 -i ../kbd-2.2.0-backspace-1.patch
```

After patching, the Backspace key generates the character with code 127, and the Delete key generates a well-known escape sequence.
Remove the redundant resizecons program (it replaces the defunct svgalid to provide the video mode files - for normal using setfonts the console appropriately) together with its manageap.

```
sed -i '/\(RESIZECONS_PROGS=\\)/yes\/no/g' configure
sed -i '/s/resizecons.8 //' docs/man/man8/Makefile
```

Prepare Kbd for compilation:

```
PKG_CONFIG_PATH=/tools/lib/pkgconfig .configure --prefix=/usr --disable-vlock
```

The meaning of the configure options:

```
--disable-vlock
This option prevents the vlock utility from being built, as it requires the PAM library, which isn't available in the chroot environment.
```

Compile the package:

```
make
```

To test the results, issue:

```
make check
```

Install the package:

```
make install
```

> Note
For some languages (e.g., Belarusian) the Kbd package doesn't provide a useful keymap for the stock "by" keymap assumes the ISO-8859-5 encoding, and the CP1251 keymap is normally used. Users of such languages have to download working keymaps separately.

If desired, install the documentation:

```
mkdir -v /usr/share/doc/kbd-2.2.0
cp -R -v docs/doc/* /usr/share/doc/kbd-2.2.0
```