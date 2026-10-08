# 6.70. Texinfo-6.6

The Texinfo package contains programs for reading, writing, and converting info pages.

Approximate build time: 0.8 SBU
Required disk space: 122 MB

# 6.70.1. Installation of Texinfo

Prepare Texinfo for compilation:

```
./configure --prefix=/usr --disable-static
```

The meaning of the configure options:

--disable-static
In this case, the top-level configure script will complain that this is an unrecognized option, the configure script for XSPParagraph recognizes it and uses it to disable installing a static XSPParagraph.a to /usr/lib/texinfo.

Compile the package:

make

To test the results, issue:

make check

Install the package:

make install

Optionally, install the components belonging in a Tex installation:

make TEXMF=/usr/share/texmf install-tex

The meaning of the make parameter:

TEXMF=/usr/share/texmf
The TEXMF variable holds the location of the root of the TeX tree, for example, a TeX package will be installed later.

The documentation system uses a plain text file to hold its list of menu entries. The file is located at /usr/share/info/dir. Unfortunately, due to occasional problems in the Makefiles of various packages, it can get out of sync with the info pages installed on the system. If the /usr/share/info/dir ever needs to be recreated, the following optional commands will accomplish the task:

```
pushd /usr/share/info
rm -v dir
for f in *
  do install-info $f dir>/dev/null
done
popd
```