# B.3 Installing Tcl/Tk on Unix/Linux Systems

Configuration:
--cache-file=FILE
--help
--no-create
--quiet, --silent
--version

cache test results in FILE
print this message
do not create output files
do not print 'checking...' messages
print the version of autoconf
that created configure

Directory and file names:
--prefix=PREFIX
--exec-prefix=PREFIX

install architecture-independent
files in PREFIX
[/usr/local]
install architecture-dependent files
in PREFIX
[same as prefix]

--srcdir=DIR
--program-prefix=PREFIX prepend PREFIX to installed
program names
--program-suffix=SUFFIX append SUFFIX to installed
program names
--program-transform-name=PROGRAM run sed PROGRAM on installed
program names

Host type:
--build=BUILD
[BUILD-HOST]
--host=HOST
--target=TARGET

configure for building on BUILD
configure for HOST [guessed]
configure for TARGET [TARGET=HOST]

Features and packages:
--disable-FEATURE
--enable-FEATURE=[ARG]
--with-PACKAGE=[ARG]
--without-PACKAGE
--x-includes=DIR
--x-libraries=DIR
--enable and with options recognized:
--enable-gcc
--disable-load
--enable-shared

do not include FEATURE (same as
--enable-FEATURE=no)
include FEATURE [ARG=yes]
use PACKAGE [ARG=yes]
do not use PACKAGE (same as
--with-PACKAGE=no)
X files are in DIR
X library files are in DIR
allow use of gcc if available
disallow dynamic loading and load
command
build libtcl as a shared library

633