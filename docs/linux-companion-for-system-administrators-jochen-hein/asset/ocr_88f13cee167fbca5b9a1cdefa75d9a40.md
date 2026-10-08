# INSTALLATION OF PROGRAMS 329

GNU programs are normally installed in the /usr/local directory. Under LINUX, the GNU programs are often installed in the /usr directory like the standard programs. This is achieved with the option --help (Listing 11.5). The command ./configure --help produces a list of all supported options. In addition, you can find the available options (for example, for setting the path to the X libraries) together with further explanations in the INSTALL README files.

```
(Linux):"gzip-1.2.4> /configure --prefix=/usr
```

**Listing 11.5** The option --prefix of the configure call.

Subsequently, the program can be compiled by means of make and installed by means install. GNU programs are normally compiled in such a way that a debugger can be used to detect errors. For the average system administrator, this is not needed, and it takes up a lot of space on the hard disk. There are two ways to remedy this. First of all, environment variables can be set, for example by entering them in the initialization files of the shell (Listing 11.6).

```
(Linux):"/gzip-1.2.4> setenv CFLAGS=-O2
(Linux):"/gzip-1.2.4> setenv LFLAGS=-a
```

**Listing 11.6** Additional flags for C compiler and linker.

The variables can also be specified at the call of the make program in addition to the corresponding target (Listing 11.7). For all GNU programs, you can store such settings in the file /etc/config.site, which is read by all configure scripts.

Now the program is installed. On the shell, it may be necessary to rebuild the hash table in which the shell stores the paths to programs. In the tash, this is done with the command hash, in the bash with hash -r.

Some GNU packages, such as the GNU C compiler (GCC) or the Emacs editor, can be configured with a series of additional options. Precise information on the possible and mandatory options of the configure script can be found in the INSTALL file which is included in each package.

The GNU build system is very versatile. It consists of autoconf which creates configure scripts, automake which helps to create Makefiles, and libtool which can create shared libraries on lots of systems. With these tools in place, porting programs can be very easy.

Programs do not depend on an Operating System; they depend on features. configure checks for those features and creates a file, config .h,