# Downloading and Compiling Sendmail

Making in ..obj.Linux.2.2.10.i586/libmsutil
make[1]: Entering directory
/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/libmsutil
cc 0 -I. -I../-I../sendmail -I../-include -DNDEWEB
DOT_SENDMAIL -c debug -o debug.o
cc 0 -I. -I../-I../sendmail -I../-include -DNDEWEB
DOT_SENDMAIL -c errstring.c -o errstring.o
Many, many, many lines deleted...
cc 0 -I. -I../-I../sendmail -I../-include -DNDEWEB
DOT_SENDMAIL -c vacation.o -o vacation.o
cc vacation.o
/../libmsdb/libmsdb.a
/../libmsutil.a -ldb -lcrypt -lnsl -1dl
group -Tascii -man vacation.1 > vacation.0 ||
cp vacation.0 dist vacation.0
make[1]: Leaving directory

Build the architecture of the system and builds the correct Makefile for your system. It compiles Sendmail using the newly created Makefile.

According to the documentation, running Build is all you need to do on most systems to compile Sendmail. It works wonderfully on Calder Linux systems, as example illustrates. However, the installation notes warn of several possible problems that can occur with some Linux systems, are described in the next section, "Known Problems."

Once Sendmail compiles, it is installed using the Build command with the install option (see Listing 3.12).

# 3.12 Installing the New Sendmail Binaries

```
# ./Build install
Making in:
/usr/local/src/sendmail-8.11.0/libmsutil
Configuration: pfx*, linux=2.2.10, rbase=2, rroot=2.2,
arch=i586, sfx=, variant=optimized
Making in ..obj.Linux.2.2.10.i586/libmsutil
make[1]: Entering directory
/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/libmsutil
.. Many, many, many lines deleted...
Making in ..obj.Linux.2.2.10.i586/vacation
make[1]: Entering directory
/usr/local/src/sendmail-8.11.0/obj.Linux.2.2.10.i586/vacation
install -c -o bin -g -m 555 vacation /usr/bin
```