```
[-defsym symbol=expression] [--demangle]
[--no-demangle] [-e emed] [--embedded-relocs] [-E]
[--export-dynamic] [-f name] [--auxiliary name]
[-F name] [--filter name] [--format input-format]
[-g] [--g-size] [-h name] [--soname name] [--help]
[-i] [--l] [--searchdir] [-M] [--Map mapfile]
[-m emulation] [-n] [-N] [--noinhibit-exec]
[--no-keep-memory] [--no-warn-mismatch] [--olevel]
[--format output-format] [-R file name] [--relax]
[-r] [--Ur] [--rpath directory] [--rpath-link directory]
[-S] [-s] [--shared] [--sort-common]
[--split-by-reloc count] [--split-by-file]
[-T commandfile]
[--section-start sectionname=sectionorg]
[--text textorg] [--Tdata dataorg] [--Tbss bssorg]
[-t] [--trace] [-v] [--verbose] [--version]
[--warn-common] [--warn-constructors]
[--warn-multiple-gp] [--warn-once]
[--warn-section-align] [--whole-archive]
[--no-whole-archive] [--wrap symbol] [-X] [-x]
```

Although that looks like a lot of command-line parameters, in reality you should not have to use very many of them at any one time. The example just shows that the GNU linker is an extremely versatile program and has many different capabilities. Table 27-3 describes the command-line parameters that are used for the Intel platform.

| **Parameter** | **Description** |
|---|---|
| `-b` | Specify the format of the object code input files |
| `-Bstatic` | Use only static libraries |
| `-Bdynamic` | Use only dynamic libraries |
| `-Bsymbolic` | Bind references to global symbols in shared libraries |
| `-c` | Read commands from the specified command file |
| `--cref` | Create a cross-reference table |
| `-d` | Assign space to common symbols even if relocatable output is specified |
| `-defsym` | Create the specified global symbol in the output file |
| `--demangle` | Demangle symbol names in error messages |
| `-e` | Use the specified symbol as the beginning execution point of the program |
| `-E` | For ELF-format files, add all symbols to the dynamic symbol table |
| `-f` | For ELF-format shared objects, set the DT_AUXILIARY name |