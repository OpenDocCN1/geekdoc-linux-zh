| SPARCworks | GNU gld | Description |
|---|---|---|
| `-a` | `-static` | Enable the default behavior in the static mode and prevent linking with the shared libraries. The linker is creating an executable and undefined symbols cause error messages. |
| `-b` |  | Achieve the equivalent of the GNU linker by not compiling the source code with the options `-fPIC` or `-fpic`. |
| `-g` | `-g` | Produce debugging information in the operating system native format. |
| `-m` | `(-M)` | Print a linker map. The `-M` option prints something comparable but with a different format and slightly different content. |
| `-s` | `-S/-s` | Achieves the equivalent of the `-s` option by using `-S` with the GNU linker, which removes only the debugging information. |
| `-h name` | `-soname name` | Set `name` as the shared object name. |
| `-o filename` | `-o filename` | Place output in a file. This applies regardless of the type of output being produced. The default is to put an executable file in `a.out`. |
| `-L dir` | `-Ldir` | Add directory `dir` to the list of directories. |
| `-R path` | `-rpath path` | Specify the search path for the runtime linker. |