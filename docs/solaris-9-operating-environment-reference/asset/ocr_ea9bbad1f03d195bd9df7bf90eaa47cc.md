# 662

# ld.so.1

However, the user compatibility library is intended neither to enable the generation of such applications nor to endorse this particular programming practice.

# Environment Variables

**LD_AUDIT** Specify a colon-separated list of objects that are loaded by the runtime linker. As each object is loaded, it is examined for Link-Auditing interfaces. The routines that are present are called specified in the Link-Auditing interface described in the *Linker and Libraries Guide*.

**LD_BIND_NOW** Override the runtime linker's default mode of performing lazy binding by setting the environment variable `LD_BIND_NOW` to any non-null value. With this setting, the runtime linker performs both data and function reference relocations during process before transferring control to the application. Also see the `-z now` of `ld(1)`

**LD_CONFIG** Provide an alternative configuration file. You can use configuration files to alter default search paths, provide a directory cache, and provide alternative object dependencies. See `conf(1)`. New in the Solaris 8 release

**LD_DEBUG** Specify a comma-separated list of tokens so that the runtime linker can print debugging information to the standard error. The `help` special token shows the full list of tokens available. You can also supply the environment variable `LD_DEBUG_OUTPUT` to specify a file to which the debugging information is sent. The file name is suffixed with the process ID of the application generating the debugging information.

**LD_DEMANGLE** Show any symbol name used as part of a diagnostic message as it is defined within an ELF file. When you set `LD_DEMANGLE` the runtime linker tries to decode (demangle) any C++ symbol names. New in the Solaris 8 release

**LD_FLAGS** An alternative way to supply environment variable information. You can specify any of the `LD_XXX` environment variables as an xxx token. Separate multiple tokens with commas. New in the Solaris 8 release

**LD_LIBRARY_PATH** Enhance the search path that the runtime linker uses to find dynamic dependencies. `LD_LIBRARY_PATH` specifies a colon-separated list of directories that are to be searched before the default directories. Also note that `LD_LIBRARY_PATH` adds তেমনি to `ld(1)`.

**LD_LOADFLTR** Set to any non-null value to process filters immediately when they are loaded. Filters are a form of shared object. They enable an alternative shared object to be selected at runtime and provide the implementation for any symbols defined within the filter. See the -