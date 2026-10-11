The configure file is a script that does two things when it is run. First, it checks your system to make sure all the necessary components required to compile the program are available. One of the most important things it checks for is the existence of a compiler compatible with the C programming language. If you don't have a C compiler, such as the GNU C Compiler (gcc) or the GNU C++ Compiler (gcc-c++), the configure command will display an error on the screen instructing you to install a compiler and then run configure again. It also verifies that your overall system environment is compatible with the program you're going to install.

Second, it also creates a very important file called Makefile. Because most source code applications are designed to be deployed on a variety of distributions and architectures, the installation program needs to know how to customize the source code files such that the resulting executable will run on your particular system. One of the last things the configure script does is create a series of Makefile files. The Makefile file contains specific instructions for how the executable should be compiled to run on your platform.

While not required, it's usually a good idea to check the Makefile after running configure to verify that the program is going to be installed in the manner you want. If you see something you want to change, you can use a text editor to make the appropriate changes and save the file.

Once configure has been run and the Makefile is ready, the next step in the process is to actually compile the executable. Let's discuss how this is done next.

# ## Compiling the Executable

At this point in the process, the program you want to install still exists only as source code in your file system. Before you can run it, you must convert the text-based source code into a binary executable file. This is done using the make command. The make command calls your system's C compiler (such as gcc) and directs it to read the source code files, using the specifications and options listed in the Makefile file, and generate a compiled executable file. This is done by entering make at the shell prompt without any options while you are still in the directory created when you untarred the tarball file. Here is an example:

```
wsl:/home/tux/Downloads/pure-ftpd-1.0.29 $ make
make all-recursive
make[1]: Entering directory `/home/tux/Downloads/pure-ftpd-1.0.29'
Making all in puredb
make[2]: Entering directory `/home/tux/Downloads/pure-ftpd-1.0.29/puredb'
Making all in src
make[3]: Entering directory `/home/tux/Downloads/pure-ftpd-1.0.29/puredb/src'
gcc -DRAVE_CONFIG_H -I.. -I../ -I/usr/local/include -DCONFDIR="/etc/" -DSTATE_DIR="/var" -g -02-MP puredb_read.c -MD-MP -deps/puredb_read.Tpo -c -o puredb_read.o puredb_read.c
tw -f .deps/puredb_read.Tpo .deps/puredb_read.o
rm -f libpuredb_read.a
ar cru libpuredb_read.a puredb_read.o
...
```