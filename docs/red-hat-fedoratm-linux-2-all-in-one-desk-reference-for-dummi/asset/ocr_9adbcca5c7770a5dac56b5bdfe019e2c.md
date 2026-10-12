Although these steps are specific to XMS, most other packages follow these steps — `configure`, `make`, and `install`. The `configure` shell script guesses system-dependent variables and creates a `Makefile` with commands needed to build and install the software.

Usually, you don't have to do anything but type the commands to build the software, but you must install the software-development tools on your system. You must install the Software Development package when you install Fedora Core. To build and run XMS, you must also install the X Software Development package because it's an X application.

To begin building XMS, type the following command to run the `configure` script (you must be in the `xms-1.2.10` directory when you type this command):

```
./configure
```

The `configure` script starts running and prints lots of messages as it checks various features of your system — from the existence of the C compiler to various libraries needed to build XMS. Finally, the `configure` script creates a `Makefile` you can use to build the software.

If the `configure` script displays error messages and fails, review the `INSTALL` and `README` files to find any clues to solving the problem. You may be able to circumvent it by providing some information to the `configure` script through command-line arguments.

After the `configure` script finishes, build the software by typing `make`. This command runs the GNU `make` utility, which reads the `Makefile` and starts compiling the source files according to information specified in the `Makefile`. The `make` command goes through all the source directories, compiles the source files, and creates the executable files and libraries needed to run XMS. You see a lot of messages scroll by as each file is compiled. These messages show the commands used to compile and link the files.

The `make` command can take 10 to 15 minutes to complete. After `make` is done, you can install the XMS software with the following command:

```
make install
```

This command also runs GNU `make`, but the `install` argument instructs GNU `make` to perform a specific set of commands from the `Makefile`. These instructions essentially go through all the subdirectories and copy various files to their final locations. For example, the binary executable files `xms`, `gnomexms`, `wmxms`, and `xms-config` copy to the `/usr/bin` directory.