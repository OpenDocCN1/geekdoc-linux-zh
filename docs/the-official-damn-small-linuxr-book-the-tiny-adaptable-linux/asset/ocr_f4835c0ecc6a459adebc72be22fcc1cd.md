In fact, the tar.gz as defined and used in DSL is much closer to the relocatable application concept first used by the RISC OS and later adopted by Apple’s MAC OSX as application directories.

Having self-contained applications means simple installation and removal. No package manager needed. No dependencies to manage. Because all the files in DSL tar.gz extensions are contained in one directory structure, compressing those extensions into a uci type becomes trivial. Alas, these self-contained applications are either not popular or not available on Linux-based systems.

You are left with compiling from source. With the use of compiler make options, by compiling from source you can force the application to be relocated into the native write-enabled area of DSL, /opt.

# Compiling from Source to Create a TAR.GZ Extension

Although it is beyond the scope of this single chapter to cover all aspects of compiling Linux source files, the purpose is to illustrate the concepts that would apply to DSL. I will again use the now familiar application of Zile.

Let’s review why we might choose to go with a .tar.gz extension rather than the previously discussed .dsl extension. The primary reason is the issue of memory usage. Using only the natively write-enabled areas of DSL means the .tar.gz extension type does not need to force other areas of the file system to be write-enabled. As previously mentioned, writing files over existing system files can cause system instability.

By definition, the .tar.gz extension has write access to /opt, /tmp, and /home (/etc is possible, but not recommended due to lack of RAM space).

On the other hand, there are not many readily available self-contained applications. Sometimes, you can take a large binary executable, with its unique required libraries, and force it as a .tar.gz by using wrapper startup script. This script can force its library search path elsewhere by using the LD_LIBRARY_PATH environment variable. Although this is possible, it is not recommended because its nonstandard setup is usually not general enough for more than a specific use.

For these reasons, we recommend compiling from source. I will now describe how to build Zile from an existing live CD-ROM of DSL:

+   1. Boot DSL with the now familiar base norestore legacy options. You do this to ensure no accidental dependencies are introduced and that the extension will work all versions, installations, and runtime options of DSL.