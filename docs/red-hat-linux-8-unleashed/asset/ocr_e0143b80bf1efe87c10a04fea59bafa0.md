# CHAPTER 27 Using Emulators and Other Cross-Platform Tools in Red Hat Linux

You install the Cygwin distribution by downloading it and then running an installer named setup.exe. The installer then downloads and installs the portions of the Cygwin package that you indicate to install. The default installation location under Windows is C:\cywin. The Cygwin DLL works with all non-beta, x86 versions of Windows since Windows 95, with the exception of CE.

Source code for all the installed software is also available from Cygwin and you can use your existing development tools to modify existing programs or build new applications in Cygwin. The list of GNU and open source software is extensive, and includes many commands and clients in the following categories:

+   - Document and graphics utilities, such as GNU ghostscript
- GNU file utilities, such as bzip2, gzip, tar, cpio
- Internet utilities for Web browsing, FTP, and electronic mail
- OpenSSH clients as ssh, sftp, and scp
- Ports of the GNU software development tools, such as gcc and autoconf
- Shells, such as ash, and zsh
- Software libraries for client and development
- System scheduling software such as cron
- Text editors, such as ed, nano, emacs, and vim
- The Apache Web server and related commands, such as curl and wget
- Various networking tools
- X Window System and related software, such as a server, window managers, and clients

# Cross Compilers and Other Cross-Platform Tools for Use in Red Hat Linux

Cross-compilers allow you to compile non-native binaries on a platform that is inexpensive, fast, or convenient (such as a Linux on Intel hardware) and that will run on a completely different architecture. Linux was first cross-compiled on a minix system.

For developing Palm Pilot applications, a cross compiler makes perfect sense (because you can't develop apps on a Palm Pilot, you can only run them). If you are a developer with a PalmOS PDA, browse to http://www.palmos.com/dev/tools/gcc/ to download Linux development tools for building PalmOS applications free of licensing fees or royalties.