# 706

# localedef

# Options

+   -c Create permanent output even if warning messages have been issued.

+   -C compiler-options Pass the compiler-options to the C compiler (cc). If you specify more than one option, you must enclose all of them in quotes ("*").

This option is starting with the Solaris 8 release. Instead, use the -W cc, option.

+   -f charset Specify the path name of a file containing a mapping of character symbols and collating element symbols to actual character encodings. You must specify this option if you use symbolic names (other than collating symbols defined in a collating-symbol keyword). If you do not use the -f option, use the default character mapping.

+   -i sourcefile Specify the path name of a file containing the source definitions. If you do not use this option, read source definitions from standard input.

+   -L linker-options Pass the linker-options to the C compiler (cc) that follows the C source file name. If you specify more than one option

This option is starting with the Solaris 8 release. Instead, use the -W cc, option.

+   -m model Specify whether localedef generates a 64-bit or a 32-bit local object. To generate a 32-bit object, specify model as ip32. To generate a 64-bit local object, specify lp64. The default is -m ip32.

+   -W cc, arg Pass arguments to the C compiler separating the preceding with a comma. (You can make a comma part of an argument by immediately preceding it with a backslash character to escape it. The backslash is removed from the resulting argument.)

+   Use this option instead of the -C and -L options, starting with the Solaris 8 release.

+   -x extensions-file Specify the path name of an extension file where various localedef options are listed. See localedef(5).

If you specify the -c option and warnings occur, permanent output is created. The following conditions issue warning messages.

+   * Use a symbolic name not found in the charset file for the descriptions of the LC_CTYPE or LC_COLLATE categories (for other categories, this is an error condition).

+   * If optional keywords not supported by the implementation are present in the source.