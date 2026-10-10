| Option | Description |
|---|---|
| `--with-install-root` | the root, where to install to [default=/] |
| `--disable-rpath` | do not use the rpath feature of ld |
| `--with-xmldir` | if the xdm config dir can't be found automatically |
| `--without-pam` | disable Pluggable Authentication Modules |
| `--with-shadow` | if you want shadow password support |
| `--without-gl` | disable 3-D GL modes |
| `--without-xpm` | disable color pixmap XPM tests |

Several options are not required and are only useful as workarounds for known problems (e.g., `--disable-path-check`). Since some are important options, for instance `--with-Shadow`, you should always check the available options.

An important option is `--prefix`. This option specifies the path where configure should install (for `kdesupport` and `kdellibs`) or where to look for libraries (for the other packages). By default, configure will look in `/usr/local/kde`. If you want to install KDE into `/opt/kde`, you have to use `configure --prefix /opt/kde`.

If you have installed the Qt libraries in an uncommon place, for instance in `$HOME/src/qt`, you must use `configure --with-qt-dir=$HOME/src/qt`. By default configure looks in the most common places for QT before it gives up.

If you have problems that you are not able to solve, send a copy of the file `config.log` to the address in the README file in the offending package.

You must install KDE in the following order: `kdesupport`, `kdellibs`, then the application packages (for example `kdbase`). All of the application packages should only depend on `kdellibs`, so you can compile them at the same time (if you have a powerful machine).

If you want to take advantage of multiprocessor systems, try make `-j <Number of processors>` instead of make.