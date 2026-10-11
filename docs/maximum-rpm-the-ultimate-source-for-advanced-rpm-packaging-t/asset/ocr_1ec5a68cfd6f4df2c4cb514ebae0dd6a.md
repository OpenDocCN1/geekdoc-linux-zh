The following flags are currently defined:

+   1. \texttt{RPMINSTALL\_REPLACEPKG}---Install the package even if it is already installed.
+   2. \texttt{RPMINSTALL\_REPLACEFILES}---Install the package even if it will replace files owned by another package.
+   3. \texttt{RPMINSTALL\_TEST}---Perform all install-time checks, but do not actually install the package.
+   4. \texttt{RPMINSTALL\_UPGRADE}---Install the package, and remove all older versions of the package.
+   5. \texttt{RPMINSTALL\_UPGRADETOOLD}---Install the package, even if the package is an older version of an already-installed package.
+   6. \texttt{RPMINSTALL\_NODOCS}---Do not install the package's documentation files.
+   7. \texttt{RPMINSTALL\_NOSCRIPTS}---Do not execute the package's install- and erase-time (in the case of an upgrade) scripts.
+   8. \texttt{RPMINSTALL\_NOARCH}---Do not perform architecture-compatibility tests.
+   9. \texttt{RPMINSTALL\_NOOS}---Do not perform operating system--compatibility tests.

The \texttt{notify} parameter is used to specify a progress-tracking-function that will be called during the installation. See section 21.2.8.3 for more information on this parameter.

The \texttt{labelFormat} parameter can be used to specify how the package label should be formatted. This information is used when printing the package label once the package install is ready to proceed. If \texttt{labelFormat} is NULL, the package label is not printed.

The \texttt{netsharedPath} parameter is used to specify that part of the local filesystem that is shared with other systems. If there is more than one path that is shared, the paths should be separated with a colon.

This function returns the following status values:

+   1. 0---The binary package was installed successfully.
+   2. 1---The binary package file contained incorrect magic numbers.
+   3. 2---Another type of error occurred.

# 21.2.8.3. rpmNotifyFunction()---Track Package Installation Progress

A function can be passed to \texttt{rpmInstallSourcePackage} or \texttt{rpmInstallPackage} via the notify parameter:

```
```C
#include <rpm/rpmlib.h>

typedef void (*rpmNotifyFunction)(const unsigned long amount,
                                const unsigned long total);
```
```