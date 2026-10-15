+   1. Head to http://www.ardi.com/download.html. Alternately, you can look in the /Executor directory of the included CD-ROM.

+   2. Select the Linux version of Executor most appropriate to your system. Chances are this will be Linux glibc RPM. Select a download site as well.

+   3. The download should result in a file named something like executor-xxxx-glibc-demo-i386.rpm.tar.gz with the version number replacing the xxxx. Place this in a convenient directory.

+   4. Extract the archive you just downloaded with the command tar -zxvf executor-xxxx-glibc-demo-i386.rpm.tar.gz, replacing the xxxx with the actual version number in the filename. You should see four or five new RPM files.

+   5. There are three versions of Executor: standard, SDL (Simple DirectMedia Layer), and SVGA. Do not use the obsolete SVGA version. If possible, you should install the SDL version.

> The upcoming installation steps might require that you use the su command for root-level access.

+   6. Install the SDL system by typing rpm --install SDL-1.0.6-1.i386.rpm. (The version number might be slightly different.)

+   7. Install the Executor support files with rpm --install executor-aux-2.1pr11-1.noarch.rpm. (Again, the version number might be different.)

+   8. Install Executor itself with the command rpm --install executor-glibc-demo-ds1-2.1pr11-1.i386.rpm. (Substitute the proper version number if necessary.)

+   9. Executor is installed and can be invoked with the command executor-demo-sdl at any command prompt. (If you find it necessary to install the plain version of Executor, the command is executor-demo.)

# Running Macintosh Programs in Executor

When you run Executor, you should briefly see a graphical splash screen, followed by an About box containing information about the demo version and ordering information, as shown in Figure 17.4.

Executor can see your Linux file system without any network trickery or user intervention. Indeed, as part of the installation process, ARDI creates a new directory at /home/executor and fills it with sample Mac programs that work well in the emulator. See Figure 17.5 for an example.

You can use the Browser to install or copy new Macintosh programs to your Linux hard drive (in the special /home/executor directory, if you want to keep things organized).