some other method of contacting the author in case you absolutely cannot get the program to work. Poorly written programs do not provide all this information. Try to make sure that the programs you obtain either include such documentation or provide the author's contact information.

The INSTALL file explains how to compile the program correctly and also lists other programs needed for this program to work. Usually the INSTALL file also lists all the types of machines on which this program has been tested and has been proven to work. Some other notes included in the INSTALL file explain the various types of flags or options that can be listed with the .configure command that the system might require to compile the program correctly. For example, rather than editing the Makefile and changing the default installation location you can add a --prefix=/usr/local/etc or other variable to change the default location. Or should the system require a particular type of C compiler and its location, or if it allows you to enable a certain feature such as sound or compatibility with other libraries, these options would normally be listed in the INSTALL file. Also, most programs grant you the option of linking to other libraries if necessary. Basically, the INSTALL file describes most of the steps needed to install and compile your new program correctly.

When you install Window Maker or any other program that depends upon other programs to function, you will discover that to compile the program correctly, you must install additional libraries beforehand. One of those libraries that was previously included with the program is now listed separately to avoid forking the project or causing unnecessary splits and divergences in program development. The INSTALL file lists exactly those files upon which Window Maker relies. One of those files is libPropList.

# ## Configuring Dependent Libraries Beforehand

The following is a quick and easy method to perform an initial install before compiling Window Maker:

+   1. Change directories one level up so that when you issue a `pwd` command you can see that your current location is `/usr/local/gnu`.

+   2. Untar and gunzip the `libPropList-0.10.1.tar.gz` file, which creates a directory with the same name.

+   3. Change to the new directory and read the INSTALL file there just as you did with the `WindowMaker` file. The instructions are very simple