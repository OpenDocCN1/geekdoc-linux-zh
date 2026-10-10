This prints pre-processor and compile flags required to compile the packages on the command line, including flags for all their dependencies. Flags are “compressed” so that each identical flag appears only once. *pkg-config* exits with a nonzero code if it can’t find tadata for one or more of the packages on the command line.

+   —*cflags-only-I*

+   This prints the -I part of “—cflags”. That is, it defines the header search path but doesn’t specify anything else.

+   —*cflags-only-other*

+   This prints parts of “—cflags” not covered by “—cflags-only-I”.

+   —*libs*

+   This option is identical to “—cflags”, only it prints the link flags. As with “—cflags”, duplicate flags are rged (maintaining proper ordering,)), and flags for dependencies are included in the output.

+   —*libs-only-L*

+   This prints the -L/-R part of “—libs”. That is, it defines the library search path but doesn’t specify which libraries to link with.

+   —*libs-only-I*

+   This prints the -l part of “—libs” for the libraries specified on the command line. Note that the union of “—libs-only-I” and “—libs-only-L” may be smaller than “—libs”, due to flags such as -rdynamic.

+   —*libs-only-other*

+   This prints the parts of “—libs” not covered by “—libs-only-L” and “—libs-only-I”, such as “—pthread”.

+   —*variable=VARIABLENAME*

+   This returns the value of a variable defined in a package’s .pc file. Most packages define the variable “prefix”, for example, so you can say: `$ pkg-config --variable=prefix glib-2.0 /usr/`

+   —*define-variable=VARIABLENAME=VALUE*

+   This sets a global value for a variable, overriding the value in any .pc files. Most packages define the variable “prefix”, for example, so you can say: `$ pkg-config --print-errors --define-variable=prefix=/foo \ --variable=prefix glib-2.0 /foo`

+   —*print-variables*

+   Returns a list of all variables defined in the package.

+   —*uninstalled*

+   Normally if you request the package “foo” and the package “foo-uninstalled” exists, *pkg-config* will prefer the “-uninstalled” variant. This allows compilation/linking against uninstalled packages. If you specify the “—uninstalled” option, *pkg-config* will return successfully if any “-uninstalled” packages are being used, and return failure (false) otherwise. (The PKG_CONFIG_DISABLE_UNINSTALLED environnt variable keeps *pkg-config* from implicitly choosing “-uninstalled” packages, so if that variable is set, they will only have been used if you pass a na like “foo-uninstalled” on the command line explicitly.)

+   —*exists*