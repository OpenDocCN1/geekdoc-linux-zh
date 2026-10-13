# LISTING 17.1 CONTINUED

```
```spec
%Build
./configure --prefix=/usr exec_prefix=/
make CFLAGS="$RPM_OPT_FLAGS" LDFLAGS=-s

%Install
DESTDIR=$RPM_BUILD_ROOT; export DESTDIR
make CFLAGS="$RPM_OPT_FLAGS" LDFLAGS=-s install \
prefix=$DESTDIR/usr exec_prefix=$DESTDIR/
gzip -9fn $DESTDIR/usr/info/ed.info
%Post
lisa-info install ed-section "Miscellaneous:-entry \
* - ed:(ed).                         The GNU line-oriented text editor."
%PreUn
lisa-info remove ed $1

%Files
%doc NEWS POSIX README THANKS
/bin/ed
/bin/red
/usr/info/ed.info.gz
/usr/man/man1/ed.1.gz
/usr/man/man1/red.1.gz
```
```

# FIELDS IN THE SPEC FILE

Fields are indicated with the field name followed by a colon. A pound sign (#) indicates a comment in the spec file, either in the header or in any of the sections.

Most of the fields are pieces of information that are just put into the package when it is built. However, some are used during the actual build process.

# INFORMATIONAL FIELDS

Following are descriptions of the informational fields most commonly used in a spec file:

+   - **Summary**—A one-line description of the package.
+   - **Name**—The name of the package.
+   - **Version**—The version of the software in the package.
+   - **Release**—The release number of the package. This is what you modify if you make changes to the package (that is, when the original version of the software has not changed).
+   - **Group**—The group is a multipart (usually two-part) string used by package management utilities to organize the packages into a hierarchy. The parts of the group are separated by a slash. For example, the ed package is in the Textprocessing/Editor group. A list of all the groups is available in the Groups file with your RPM documentation (usually `/usr/doc/rpm-3.0.5` if you have it installed.)
+   - **Copyright**—This indicates the copyright holder and/or the license that the software uses. Common values for the license are BSD, distributable, GPL, artistic, public domain, MIT, freeware, and shareware.