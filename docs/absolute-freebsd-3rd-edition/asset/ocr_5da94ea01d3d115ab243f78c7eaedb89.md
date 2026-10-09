This `Makefile` contains instructions for all the ports in the directory. They're more specific than the global `Makefile` in `/usr/ports`, but not as specific as individual port Makefiles. The file `Makefile.inc` contains meta-instructions for the ports in this directory. All the other directories are individual software packages. We'll dissect one of those directories in “Installing a Port” on page 371.

Individual ports are often called by their directory in the Ports Collection. The `gnuplot` graphing program might be called `math/gnuplot`, as its port can be found at `/usr/ports/math/gnuplot`.

# ## The Ports Index

The ports index file contains a list of all ports that build on a particular FreeBSD release. On FreeBSD 13, this is `/usr/ports/INDEX-13`. The Ports Collection uses the index for several purposes, including searching the whole ports tree.

The index file describes each port on a single line, with fields separated by pipe symbols (|). While this is convenient for system tools, it's not particularly human-readable. Run `make print-index` in `/usr/ports` to get a longer, much more intelligible index. This index is filled with entries like this:

| Port: | p5-Archive-Extract-0.80 |
| Path: | /usr/ports/archivers/p5-Archive-Extract |
| Info: | Generic archive extracting mechanism |
| Maint: | perl@FreeBSD.org |
| Index: | archivers perl5 |
| B-deps: | perl5-5.24.1 |
| R-deps: | perl5-5.24.1 |
| E-deps: | |
| P-deps: | |
| F-deps: | |
| WWW: | http://search.cpan.org/dist/Archive-Extract/ |

The index starts with the port’s name and the full path to the port directory. `Info` gives a very brief description of the port. The `Maint` heading lists the port’s maintainer, a person or team who has assumed responsibility for this software’s integration into the Ports Collection. The `Index` space lists every category where this port might be filed. The