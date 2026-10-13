| Parameter | Description | Default Value |
|---|---|---|
| `--prefix=`<br>`<directory>` | Install architecture-independent files in the specified directory (this value is referred to as PREFIX in the remainder of this table) | `/usr/local` |
| `--exec-prefix=`<br>`<directory>` | Install architecture-dependent files in the specified directory (this value is referred to as EPREFIX in the remainder of this table) | The value of the `--prefix` parameter. |
| `--bindir=`<br>`<directory>` | Install user executable binary in the specified directory | `EPREFIX/bin` |
| `--sbindir=`<br>`<directory>` | Install system administration executable files in the specified directory | `EPREFIX/sbin` |
| `--libexecdir=`<br>`<directory>` | Install program executable files in the specified directory | `EPREFIX/libexec` |
| `--datadir=`<br>`<directory>` | Install read-only, architecture-independent data files in the specified directory | `PREFIX/share` |
| `--sysconfdir=`<br>`<directory>` | Install read-only single-machine data in the specified directory | `PREFIX/etc` |
| `--sharedstatedir=`<br>`<directory>` | Install modifiable architecture-independent data in the specified directory | `PREFIX/com` |
| `--localstatedir=`<br>`<directory>` | Install modifiable single-machine data in the specified directory | `PREFIX/var` |
| `--libdir=`<br>`<directory>` | Install object code libraries in the specified directory | `EPREFIX/lib` |
| `--includedir=`<br>`<directory>` | Install C header files in the specified directory | `PREFIX/include` |
| `--oldincludedir=`<br>`<directory>` | Install C header files for non-gcc compilers in the specified directory | `/usr/include` |
| `--infodir=`<br>`<directory>` | Install info style documentation in the specified directory | `PREFIX/info` |
| `--mandir=`<br>`<directory>` | Install man style documentation in the specified directory | `PREFIX/man` |
| `--srcdir=<directory>` | The directory containing the source code | The directory containing the configure script |
| `--x-includes=`<br>`<directory>` | X include files are in the specified directory |  |
| `--x-libraries=`<br>`<directory>` | X library files are in the specified directory |  |
| `--program-prefix=`<directory>` | Directory prefix for installed program names |  |
| `--program-suffix=`<directory>` | Suffix to append to installed program names |  |

**Table 25.2 — Directory and Filename Installation/Configuration Parameters**