**LSB-Embedded**   Is minimal set of interfaces that a developer targeting an embedded system would expect to be able to find. This specification module is not currently included in any product standard, but can be added to one if there is demand. In addition, this module currently includes some things that may not be present in a version used for a product standard.

**LSB-Open118N**   Provides additional internationalization commands and interfaces beyond what is included in the LSB-Core. It is to be used in conjunction with the LSB-Core module.

# 10.4  FUNCTIONAL AREA DESCRIPTIONS

A *functional area* corresponds to the smallest standards unit with reasonable justification for individual existence. To divide it into smaller units would not make sense since implementors of that interface would implement all the smaller units anyway. Often the justification for a functional area will be the possibility that it will be useful for implementors who are targeting only some portions of the available standards in an *a la carte* manner.

**Executable and Linking Format (ELF)**   Is the definition of the executable files produced by the C compilation system.

**Execution Environment**   Consists of the filesystem hierarchy, minimal granted directory and file permissions, recommendations for applications on ownership and permissions, regular expression localization, filename globbing localization, and miscellaneous API behaviors.

**Base Libraries**   Consists of libc, libm, libpthread, libgcc_s, libdl, libcrypt, libpm, and libstdcxx.

**Utility Libraries**   Consists of libz, libncurses, and libutil.

**System Initialization**   Consists of `cron` jobs, init script actions, installation, and removal of `init.d` files.