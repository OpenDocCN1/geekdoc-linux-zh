
+   2. Now you must prepare for the compilation. You should create a directory called compile inside the glibc directory with the following command:
+   `# mkdir compile`

+   3. Proceed to configure the source with the following:
+   `# cd compile`
+   `# ../configure --enable-add-ons=linuxthreads,crypt,localedata`

+   4. This will start checking your system's configuration. When it is done, run a make:
+   `# make`

+   5. This will take some time. When it is finished, you are ready to install it. This is it, the moment of truth, the point of no return. Enter the following command:
+   `# make install`

+   6. Run ldconfig to register it with Linux:
+   `# ldconfig`

Ok, try to run anything, ls for example. If it works, you are fine. Start testing your system and see how it feels after the upgrade. If it doesn't work correctly, reinstall the A series from your SuSE CD to correct the situation.

## Upgrading Your GCC

The GNU C Compiler (GCC) is your compiler package. The compilers that come with SuSE 6.2 are very good and recent. You might never need to upgrade your compiler. Currently, the latest version of GCC is 2.95. Note that this version is not a good one to have if you are going to compile your kernel.

It is best to upgrade your compilers through SuSE. When new versions of your compiler are released, SuSE will package them for you. This is the safest way to do this. To download the latest compilers from series D on the SuSE FTP site, follow the instructions at the beginning of the chapter in the section "Upgrading SuSE Linux."

If, however, you need to compile from source, you have to download the latest version of GCC from GNU. The latest compilers are found in ftp://ftp.gnu.org/gnu/gcc. You will find several files there. You can download either the whole package or just the components you need (C++ or C compiler). In this case, download the whole thing (gcc-2.95.1.tar.gz, which is around 17MB). To compile it, follow these steps:

+   1. Unpack the package to start compiling it with the following command:
+   `# tar xvfz gcc-2.95.1.tar.gz`

+   2. This will create a directory that has all the source files for the gcc package. The compilation process is quite similar to that for glibc. Please read the files in the install directory for detailed information about compiling gcc.

+   3. Next, create the compile directory by entering the following:
+      `# mkdir compile`
+   4. Configure the source files with the following:
+      `# ./configure`
+   5. Compile the package:
+      `# make bootstrap`
+   6. Or, if you are low on disk space, enter the following:
+      `make bootstrap-lean`

This will take a while to finish, especially if you issued a make bootstrap-lean. After it completes, you are ready to install the new compilers. Before you do that, though, if your previous compiler was installed using RPM, make sure you remove it using YaST before you install the new compilers to avoid a conflict.

To install the compiler, enter the following command:

```
# make install
```

That's it, GCC is installed. To check, enter this command:

```
# gcc --version
```

This will output the version number of the current compiler, which should be the new one. If you have any problems and you would like to revert to the old compiler rather than uninstall the new one, enter the following:

```
# make uninstall
```

Then, install the compilers from the SuSE CD series D again.

## Troubleshooting

*The compilation breaks with errors.*

Check what the error is; it might be due to libraries not found on your system or not properly installed. Check your libraries.

*KDE does not compile.*

Did you compile the packages in the correct order? Do that.

*GNOME does not compile.*

This is largely caused by incompatible libraries. Download the libraries that are available with the current distribution of GNOME to be safe. Remove the old ones before installing the new ones. Having multiple copies of a library can really mess up GNOME.

# *GNOME now acts weird after I upgraded it.*

Remove your local setting by deleting the .GNOME directories in your home directory. Try again.

# *The configure script fails and I am not sure why.*

Check the message it failed with, and if you still don't know why, read the contents of the file config.log. Everything the configure script does is reported in that file.

# *Ok, I fixed the problem with the configure script, but it still fails.*

Remove the file config.cache and try again.

# *Some applications don't run anymore now that I upgraded one of my libraries.*

Read the README file that came with the libraries to see whether it says anything about broken applications. Recompile the applications that don't run.

# *The kernel won't compile after I upgraded my GCC.*

Well, if you upgraded to GCC 2.95, this is expected. Revert back to the old one or compile the kernel on a different machine. ●

## Installing a New Kernel

### In this chapter

+   - Defining the Kernel 158
+   - Why Should I Install a New Kernel? 158
+   - Installing a Precompiled Kernel Versus Compiling Your Own 158
+   - Installing a Precompiled Kernel 159
+   - Installing a Kernel from Source Code 162
+   - Kernel Compilation Checklist 164
+   - Downloading and Unpacking a New Kernel 164
+   - Configuring Your Kernel 167
+   - Getting to Know the Various Important Configuration Parameters 175
+   - Behind the Scenes 181
+   - Troubleshooting 182

## Defining the Kernel

Some Linux professional users like to think that you aren't a Linux user unless you have recompiled your own kernel. Although this might be very true for them, it is not really a fact. You might never really need to recompile your kernel; it all depends on the requirements of your system. SuSE Linux specifically attempts to provide a ready-to-use kernel for several system configurations, so you can simply install one of them and start working without having to recompile your own kernel. But, of course, sometimes you will need to recompile. Reasons for this can be if you are upgrading your kernel to a newer version that offers better performance or fixes a bug you were experiencing, or if you added a new piece of hardware that needs a special driver or parameters to be built in to the kernel.

The kernel is the heart or core of the operating system. The kernel is the layer that separates the hardware layer from the applications layer. Applications that need to access the hardware do so through calls to the kernel services. The kernel then communicates or “talks” to the hardware and returns results and messages back to the application. This way, applications do not have to worry about directly talking to the hardware in its native and complex protocols; the kernel simplifies all that for the application. The kernel manages all the system resources, such as memory and CPU time. Another very important role for the kernel is to control the execution of programs (or processes) and schedule them in an efficient manner to accomplish multitasking.

## Why Should I Install a New Kernel?

The most common case in which you might want to install a new kernel is to install a new driver or component on the system. For example, if you have just purchased a new SCSI hard drive, and you never had SCSI devices on your system before, you will need to install the device driver in order for the SCSI interface to use your hard drive. This is done by configuring the kernel to include the correct SCSI interface for your hard drive and recompiling the kernel to activate that driver.

Another reason to install a new kernel is if a new release of the kernel is out and it has better performance or fixes bugs that you are experiencing. In this case, you would download that new kernel and install it on your system. And last but not least, some of us like to install new kernels just for the sake of compiling a new kernel!

## Installing a Precompiled Kernel Versus Compiling Your Own

Before you attempt to install a new kernel, you have to make an important decision. Do I have to compile my kernel? Or can I get away with a precompiled one? This is an important decision to make because your choice will dictate the process you have to go through to reach your goal. To make such a decision, you will need to have sufficient background information.
