
## INSTALLATION OF PROGRAMS 329

GNU programs are normally installed in the /usr/local directory. Under LINUX, the GNU programs are often installed in the /usr directory like the standard programs. This is achieved with the option --help (Listing 11.5). The command ./configure --help produces a list of all supported options. In addition, you can find the available options (for example, for setting the path to the X libraries) together with further explanations in the INSTALL README files.

```bash
(Linux):"gzip-1.2.4> ./configure --prefix=/usr
```

**Listing 11.5** The option --prefix of the configure call.

Subsequently, the program can be compiled by means of make and installed by means install. GNU programs are normally compiled in such a way that a debugger can be used to detect errors. For the average system administrator, this is not needed, and it takes up a lot of space on the hard disk. There are two ways to remedy this. First of all, environment variables can be set, for example by entering them in the initialization files of the shell (Listing 11.6).

```bash
(Linux):"/gzip-1.2.4> setenv CFLAGS=-O2
(Linux):"/gzip-1.2.4> setenv LFLAGS=-a
```

**Listing 11.6** Additional flags for C compiler and linker.

The variables can also be specified at the call of the make program in addition to the corresponding target (Listing 11.7). For all GNU programs, you can store such settings in the file /etc/config.site, which is read by all configure scripts.

Now the program is installed. On the shell, it may be necessary to rebuild the hash table in which the shell stores the paths to programs. In the bash, this is done with the command hash, in the bash with hash -r.

Some GNU packages, such as the GNU C compiler (GCC) or the Emacs editor, can be configured with a series of additional options. Precise information on the possible and mandatory options of the configure script can be found in the INSTALL file which is included in each package.

The GNU build system is very versatile. it consists of autoconf which creates configure scripts, automake which helps to create Makefiles, and libtool which can create shared libraries on lots of systems. With these tools in place, porting programs can be very easy.

Programs do not depend on an Operating System; they depend on features. configure checks for those features and creates a file, config.h, accordingly. These features are either reimplemented or sometimes functions of the program are disabled. The autoconf documentation describes this in detail.

## 330 TOOLS (NOT ONLY) FOR PROGRAMMERS (Wait, checking text flow...)

```bash
(Linux): ~/gzip-1.2.4> make CFLAGS=-O2 LDFLAGS=-s
(Linux): ~/gzip-1.2.4> make
(Linux): ~/gzip-1.2.4> make CFLAGS=-O2 LDFLAGS=-a install
```

Listing 11.7 Passing special flags to make.

The standard format for the documentation of GNU programs is Texinfo. This allows you to create both printed and online documentation on the basis of the same source text. Man pages are also often installed for reference, offering a brief overview of the program's options.

### 11.3.2 Installation of other programs

Programs that are not part of the GNU project are installed in many different ways. Often, a precise description of the installation is given in the README or INSTALL files. Reading these files is essential before starting the installation. Frequently, there is also a file that contains tips and tricks for individual operating systems.

One possibility for compiling programs under different UNIX systems is the creation of a Makefile for each operating system. The appropriate Makefile must be copied and, if needed, adapted. Other programs with a large Makefile which contains all configurations for the different systems. In this case, the correct setting must be activated by means of an editor.

In many cases, the programs are already prepared for compilation and installation under LINUX. Sometimes this is not the case, but often no changes are required for LINUX anyway. Usually, you can use the settings for POSIX system. If the Makefile only considers System V and BSD-based systems, you should try the System V setting. This would be sufficient to compile many of today's freely available programs. If you need to make substantial changes to the source code or the Makefiles, you should send these to the programmer. Thus, in a later version, other users can benefit from your experience.

Currently, a relatively large number of programs is being adapted for with GNU configure. This is a relatively expensive operation, but it significantly improves portability.

## 11.4 Editors

UNIX provides a very powerful environment for programmers. On the one hand, this consists of the kernel, which looks after the management of the CPU, the file system and the hardware. The kernel provides the programmer with almost all required functions. For reasons of portability and easier programming, the libc library represents a somewhat higher level of abstraction. Therefore, programmers of applications mostly use the functions of libc.

Another component of a UNIX system is the service programs. Each of these programs has been developed for a special function. By combining these programs, a series of functions can be performed with relatively little effort. The link between these programs is constituted either by pipes or by functions of the shell.

Besides these service programs and compilers, programmers also need an editor to edit their programs. Such an editor should obviously be powerful and well integrated into the UNIX environment. On every UNIX system, you will find the editor vi (or a clone). This editor is relatively small, but is very powerful and well integrated into the UNIX environment. Some hints and tips, and the most important, are presented in Appendix.

### 11.4.1 The emacs editor

One of the most widely used editors is Emacs. Because of its power and variety of features, we will introduce some aspects of this editor. Almost every programming language has its corresponding mode. With the aid of the tags mode, you can get a good overview of the implementation of Emacs. Just create a TAGS file in the Emacs directory with the command etags *.el. You can then load this file with M-x visit-tags-table and use it.

A particularly useful feature is automatic indentation. This ensures that branches and loops are (almost) always indented correctly. If you use additional syntax highlighting, you will easily find logical errors.

To save typing effort, you may be able to use abbreviation-mode. For many modes, abbreviation tables have been created that contain the keywords of the programming language.

| Key | Function | Description |
| :--- | :--- | :--- |
| M- | find-tag | Search for tag |
| C-u M- | find-tag | Next occurrence |
| | tags-search | Load files with tag |
| | tags-loop-replace | Search and replace |
| M-, | tags-loop-continue | Continue search |
| | list-tags | Display search |
| | tags-apropos | Search |

**Table 11.1** combinations for tags

The tags mode can also use a TAGS file which is stored in a different directory. This file can either be loaded manually or selected on the basis of entries in the variable tag-table-list. With the aid of the tags mode, arbitrary functions in source files can be reached with a couple of keystro.

After a program has been created, it must be compiled. For this, emacs also provides support when calling the compiler. With the command M-x compile, which can be assigned to a key combination such as C-c C-c, the compiler (precisely, the command specified in the local variable command) is started. If errors have occurred during compilation, you can use the key combination C-x' to jump to the next error position.
