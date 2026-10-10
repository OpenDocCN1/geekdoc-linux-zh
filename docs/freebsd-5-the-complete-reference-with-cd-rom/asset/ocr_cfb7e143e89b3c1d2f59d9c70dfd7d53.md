join its development team, an IDE might prove useful because you're far more likely to need to make changes to many source code files and use debugging features.

# # A Typical Software Compilation Session

The details of software compilation differ substantially from one package to another; nonetheless, certain steps are common to most or all packages. This section presents these steps, broken into four parts: obtaining the software, reading the documentation, configuring the software, and compiling the software. Of course, you must also install the software, but this step marks a turning point; before you install the software, you can easily abandon the attempt to build a text editor from scratch. After you install the software, it becomes more difficult to track down the installed files, particularly if any of these files overwrite existing files on your system.

> > **Note**  
> This section describes compiling a program without making changes to it. If you want or need to change the software, you'll use a text editor to alter the source code files.  
> For extensive changes, using an IDE can be very helpful.

# ## Obtaining the Software

The first step you must take is to obtain the software. Typically, you'll acquire the software from the developer's official web site or from an FTP archive site. Most open source program web sites include one or more download links. This description uses the Macintosh-Like Virtual Window Manager (MLVWM; http://www2u.biglobe.ne.jp/~y-miyata/mlvwm.html) 0.9.1 as a sample program. This program is large enough to require configuration but small enough that it compiles quickly, even on fairly old computers. MLVWM is a window manager that's modeled after older Macintosh systems.

> > **Note**  
> MLVWM is available as a FreeBSD package and as a port, so installing it as described here is normally not necessary.

You can download MLVWM source code from a link on the software's main page. This action creates a file called mlvwm091.tar.gz. You can examine the names of the files contained in the tarball by typing `tar tvfz mlvwm091.tar.gz | less`. This action reveals that all the files install in a directory called mlvwm091. Source tarballs usually include all their files in a subdirectory named after the program, so MLVWM is quite typical in this respect.

After examining the tarball's contents, change to a directory in which you want to store the source code. Many administrators use /usr/src for this purpose. If you want to keep source you download yourself separate from the usual FreeBSD /usr/src directory tree, you may want to use a directory in your ordinary user home directory, or perhaps /usr/local/src. You can perform most compilation steps as an ordinary user,