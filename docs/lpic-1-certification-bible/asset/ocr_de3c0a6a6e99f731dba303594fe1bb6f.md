During the install process `dpkg` will check the package for needed dependencies and display an error similar to the following if they are not installed.

```
```
debian:~# dpkg --install ethereal_0.8.13-2_i386.deb
Selecting previously deselected package ethereal.
(Reading database ... 54478 files and directories currently installed.)
Unpacking ethereal (from ethereal_0.8.13-2_i386.deb) ...
dpkg: dependency problems prevent configuration of ethereal:
 ethereal depends on libpcap0 (>= 0.4-1); however:
 Package libpcap0 is not installed.
dpkg: error processing ethereal (--install):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 Ethereal
```
```

The package `ethereal_0.8.13-2_i386.deb` requires the `libpcap0` package to be installed already, and it is not. Either install the required package separately or at the same time, as follows:

```
```
debian:~# dpkg --install ethereal_0.8.13-2_i386.deb libcap0_0.4a6-3_i386.deb
(Reading database ... 54499 files and directories currently installed.)
Preparing to replace ethereal 0.8.13-2 (using ethereal_0.8.13-2_i386.deb) ...
Unpacking replacement ethereal ...
Selecting previously deselected package libcap0.
Unpacking libcap0 (from libpcap_0.4a6-3_i386.deb) ...
Setting up libcap0 (0.4a6-3) ...
Setting up ethereal (0.8.13-2) ...
```
```

# Force options

In some cases you may need to override an error when installing or removing a package. The `dpkg` tool provides several layers of forcing so you can set which errors are ignored and which are not. Table 3-4 shows the most common options.

| Table 3-4 Common Forcing Options for dpkg |  |
|---|---|
| **Option** | **Purpose** |
| `configure-any` | Configure any other package that may help to install this package. |
| `hold` | Process another package, even if it is on hold. |
| `bad-path` | Force even when missing files. |
| `not-root` | Try to add or remove packages, even if not root. |