# 6.78. About Debugging Symbols

Most programs and libraries are, by default, compiled with debugging symbols included (with *gcc -g* option). This means that when debugging a program or library that was compiled with debugging information included, the debugger can provide only memory addresses, but also the names of the routines and variables.

However, the inclusion of these debugging symbols enlarges a program or library significantly. The following is an example of the amount of space these symbols occupy:

+   * A **bash** binary with debugging symbols: 1200 KB
* A **bash** binary without debugging symbols: 480 KB
* **Glibc** and GCC files (/lib* and */usr/lib*) with debugging symbols: 87 MB
* **Glibc** and GCC files without debugging symbols: 16 MB

Sizes may vary depending on which compiler and C libraries were used, but when comparing programs with and without debugging symbols, the difference will usually be a factor between two and five.

Because most users will never use a debugger on their system software, a lot of disk space can be regained by removing these symbols. The next section shows how to strip all debugging symbols from the programs and libraries.

# 6.79. Stripping Again

This section is optional. If the intended user is a programmer and does not plan to do any debugging on the system software, the system size can be decreased by about 90 MB by removing the debugging symbols from binaries and libraries. This causes no inconvenience other than not being able to debug the software fully anymore.

Most people who use the commands mentioned below do not experience any difficulties. However, it is easy to make a typo and render the new system unusable, so before running the **strip** commands, it is a good idea to make a backup of your LFS system in its current state.