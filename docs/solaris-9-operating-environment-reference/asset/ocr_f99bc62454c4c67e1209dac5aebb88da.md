# mdb 827

table, and standard and dynamic symbol tables for each of a number of load objects (such as shared libraries in a user process, or kernel modules in the Solaris kernel). The target typically searches the primary executable's symbol tables, and then one or more of the other symbol tables. Notice that ELF symbol tables contain entries for every, global, and static symbols; automatic symbols do not appear in the symbol tables by mdb.

Additionally, mdb provides a user-defined symbol table that is searched before any of the symbol tables. The private symbol table is initially empty; it can be manipulated with :mmadd and :mmcdms. You can use the :rim -P option to create symbols for program functions or data that were missing from the original or stripped out. These definitions are used when mdb converts a symbol name to an address, or an address to a symbol.

Each contains multiple tables and each can include symbols from multiple objects, different symbols with the same name can exist. mdb uses the character (*) as a symbol naming operator to enable you to obtain the value of the desired symbol in this situation. You can specify the symbol to resolve a symbol name as either *object name*, *file name*, or *object file name*. The object identifier refers to the name of a load object. The file identifier refers to the basename of a file that has a symbol of type ST_FILE in the specified symbol table. The object identifier's interpretation depends on the target type.

The mdb kernel expects object to specify the basename of a loaded kernel module. For example, the mdb name specs *_init evaluates the value of _init symbol in the specs kernel module.

The mdb process expects object to specify the name of the executable or of a shared library. It can take any of the following:

+   1. An exact match (that is, a full path: /usr/lib/lib.so)
2. An exact name match: lib.so.1
3. An initial match up to a . suffix: lib.so or lib
4. A literal string .out is accepted as an for the executable.

Starting in Solaris 9 release, the process target also accepts any of the four forms described above previously by an optional link-map ID (Lmid). The link prefix is specified by an initial LM followed by the link-map ID in hexadecimal by an additional backquote. For example, the example symbol

LM0:lib.so.1

evaluates the value of the _init symbol in the lib.so.1 library that is loaded on link-map 0 (LM_ID_BASE). You may need to use the link-map specifies to resolve symbol conflicts if the same library is loaded on more than one link map. For more information on link-maps, refer to the Link and Libraries Guide and dlopen(3DL). Link-map identifiers are displayed when symbols are printed according the setting of the shortmid option, described in "Options" on page 852.

When names conflict between symbols and hexadecimal values, mdb evaluates an ambiguous name as a symbol before evaluating it as an integer value. For example, the token f can refer to either the integer value 15 specified in hexadecimal (the default base) or to a global variable f in the target's symbol table. When a symbol with an ambiguous name is present, you can specify the integer value with an explicit 0x or 0 prefix.