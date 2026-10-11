# 21.2.3.2. `rpmGetBooleanVar()`—Return Boolean Value of RPM Variable

This function looks up the variable specified in `var` and returns 0 or 1, depending on the variable’s value:

```
#include <rpm/rpmlib.h>
int rpmGetBooleanVar(int var);
On error, the function returns 0.
```

# 21.2.3.3. `rpmSetVar()`—Set Value of RPM Variable

This function sets the variable specified in `var` to the value passed in `val`. It is also possible for `val` to be NULL:

```
#include <rpm/rpmlib.h>
void rpmSetVar(int var,
char *val);
```

# 21.2.4. rpmrc-Related Information

The functions in this section are all related to `rpmrc` information—the `rpmrc` files as well as the variables set from those files. This information also includes the architecture and operating system information based on `rpmrc` file entries.

# 21.2.4.1. `rpmReadConfigFiles()`—Read rpmrc Files

This function:

```
#include <rpm/rpmlib.h>
int rpmReadConfigFiles(char * file,
char * arch,
char * os,
int building);
```

reads `rpmrc` files according to the following rules:

+   - Always read `/usr/lib/rpmrc`.
+   - If file is specified, read it.
+   - If file is not specified, read `/etc/rpmrc` and `~/.rpmrc`.

Every `rpmrc` file entry is used with `rpmSetVar()` to set the appropriate RPM variable. Part of the normal `rpmrc` file processing also includes setting the architecture and operating system variables for the system executing this function. These default settings can be overridden by entering architecture and/or operating system information in `arch` and `os`, respectively. This information will still go through the normal `rpmrc` translation process.