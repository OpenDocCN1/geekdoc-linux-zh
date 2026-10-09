# Table 19-2 (Continued)

| Configuration Options | Purpose |
| :--------------------- | :--------------------------------------------------------------- |
| 386 | Use this only if you are compiling OpenSSL on an Intel 386 machine. Not recommended for newer Intel machines. |
| no-<c1ph er> | OpenSSL uses many cryptographic ciphers such as bf, cast, des, dh, dsa, hmac, md2, md5, mdc2, rc2, rc4, rc5, rsa, and sha. If you wish to not include a particular cipher in the compiled binaries, use this option. |
| -Dxxx, -Lxxx, -Lxxx, -fxxx, -Kxxx | These options allow you to specify various system-dependent options, for example, Dynamic Shared Objects (DSO) flags such as -fpic, -fPIC, and -KPIC, to be specified on the command line. This way OpenSSL libraries can be compiled with Position Independent Code (PIC), which is needed for linking it into DSOs. |

Most likely you won't need to add any of these options to compile OpenSSL. However, if you have problem compiling it, you might have to try some of these options with appropriate values. For example, if you can't compile because OpenSSL complains about missing library files, try specifying the system library path using the -L option.

After you have run the config script without any errors, run the make utility. If the make command is successful, run make test to test the newly built binaries. Finally, run make install to install OpenSSL in your system. If you have a problem compiling, try to understand the cause of the problem. In most cases, the problem is caused by library file mismatch when trying to install the latest version of software like OpenSSL in a very old Linux system. Or the problem might be caused by an option you specified in the command line. For example, if you do not have the RSAREF library (it is not included in the Red Hat Linux distribution) installed on your system and you are trying to use the rsaref option, the compilation will fail when trying to build the binaries. So make sure that you know what you are doing when using specific options. If you still can't resolve the problem, try searching on the OpenSSL FAQ page at www.openssl.org/support/faq.html for a solution. Or, simply install the binary RPM package for OpenSSL.

# Choosing the mod_ssl module for SSL support

You should use mod_ssl only if you choose not to use Apache-SSL to bring SSL support. This module can be used as a DSO module for Apache and it also works with the Windows platform.