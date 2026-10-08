
## 11.6.2 SCCS and SCSC

Commercial UNIX systems often include SCCS for version management. If you employ this system in your projects, you can use the GNU implementation SCSC under Linux. If you are beginning a new project, you should definitely look at RCS and CVS.

## Emulators under LINUX

LINUX is a largely POSIX-compatible UNIX system. This compatibility, however, is limited to the portability of C source texts between different UNIX systems. This means that many UNIX programs run under LINUX if they are recompiled on a LINUX system. This is easy for free UNIX software, but the situation is different with commercial software or programs of other systems.

Nevertheless, it is possible to run many programs under LINUX that have been created for other operating systems or even for other computer architectures. This is done using emulators, which map the functions of other hardware or other operating systems to the functions of the LINUX system.

Because of the great complexity of both LINUX and the other operating systems and processors, an emulation is often not complete. This is also because often functions must be emulated that are available and in use under other operating systems, but are not documented.

Under LINUX too, a series of emulators is available for different operating systems and computer architectures. Here, we give a more detailed presentation of the emulators for DOS, Windows, and IBC2-compatible programs. Additional emulators exist for more exotic systems, such as Macintosh, Apple II or Spectrum.

| Additional Information and Sources |
| :--- | :--- |
| ftp server: | sunsite.unc.edu |
| ftp path: | /pub/Linux/system/Emulators |

## 12.1 The BIOS emulator DOSemu

The DOSemu is not a DOS emulator, as the name suggests, but a PC and BIOS! It emulates parts of the hardware and the most important functions of the BIOS. Therefore, you need a DOS license to use it. The true DOS runs inside a user process under LINUX. You can practically use any DOS version, be MS-DOS, Novell-DOS (formerly known as DR-DOS), PC-DOS by IBM or the freely available Free DOS.

The DOS emulator is still under development. In each new version, many new functions are implemented and errors corrected (or introduced). Nevertheless, it is relatively stable, and many DOS programs also function in the emulator. In many areas, compatibility with a true DOS system is surprisingly high.

| Additional Information and Sources |
| :--- | :--- |
| Man pages: Info system: Documentation: | dos (1) Doseemu QuickStart, DANG,2 Doseemu HowTo, various README files, Novell How linux-msdos.rutgers.edu doseemu0.67.9.tar.gz |
| Mailing list: Package: Website: FreeDOS: Size: | www.doseemu.org http://www.freedos.org about 1.5 Mbytes |

### 12.1.1 Installation

The DOS emulator is still under development, no binary distribution is provided by the programmers. Some distributions include a binary version, in which case you should be able to use a relatively recent version. When you install a new kernel, problems may arise from the tight interlocking between DOSemu and the kernel.

When you install a new version of DOSemu, you must first unpack the sources on your LINUX computer and compile and install the program. First, you should configure the emulator by means of the default-configure command and then compile it. Listing 12.1 shows an example.

```
(Linux):"# cd /usr/src
(Linux):"/usr/src# tar xvf /tmp/dosemu0.067.9.tar.gz
(Linux):"/usr/src# cd dosemu-0.067.9
(Linux):"/usr/src/dosemu-0.067.9 ./default-configure
(Linux):"/usr/src/dosemu-0.067.9 make
```

Table 12.1 Configuring DOSemu.

The script configure-default automatically recognizes whether or not the X Window system is installed on the system (with header files and libraries) and if this is the case, also generates an emulator that can run under X. Additional settings which must be carried out at compile time are set to default values. Table 12.1 shows a selection of the possible configuration options.

| Option | Meaning |
| :--- | :--- |
| --enable-novm8plus | The new variation for switching into vm86 mode is not used |
| --with-x=[yes|no] | With/without X support |
| --enable-nomitshm | Do not employ shared memory during X access |
| --enable-debugbug | Activate debugging |
| --enable-nosbem | Do not activate Soundblaster emulation |
| --enable-linkstatic | Link statically |
| --enable-runroot | Installation as setuid program |

Table 12.1 Options for the DOSemu configure script.

Any further configuration of the emulator can be carried out by means of the configuration file /etc/dosemu.conf or ~/.dosrc, so that it is not necessary to make changes to the Makefile file.

### 12.1.2 Configure the emulator

After installation, only the configuration files for the emulator need to be adapted. First of all, the names of all users who are allowed to start the DOS emulator must be registered in the file /etc/dosemu.users. This allows use of the emulator to be restricted to 'trustworthy' users. For many functions, such as graphical output or access to ports, it is necessary to start the emulator with root privileges. This restriction to describe named users helps to alleviate this security problem.

With certain restrictions, which are essentially dictated by security considerations, users can carry out the configuration of the DOS emulator by creating a file .dosrc in their home directory. The system administrator can carry out a system-wide configuration for all users with the aid of the file /etc/dosemu.conf. The syntax of both files is identical; the file ./examples/config.dist from the source distribution of the DOS emulator can serve as an example.

The configuration can be carried out with any editor of your choice. It is also possible to use the .configure script, which can be found in the sources of the emulator. In that case, however, the file will not contain all the comments which extensively describe the possible options in the sample file. Furthermore, you will not find the examples that have been commented out, so the entries cannot immediately be recognized. Even a modification carried out at a later stage becomes more difficult, because the configuration program does not read an existing configuration file a second time.

The configuration can be carried out with any editor of your choice. It is also possible to use the .configure script, which can be found in the sources of the emulator. In that case, however, the file will not contain all the comments which extensively describe the possible options in the sample file. Furthermore, you will not find the examples that have been commented out, so the entries cannot immediately be recognized. Even a modification carried out at a later stage becomes more difficult, because the configuration program does not read an existing configuration file a second time.

The configuration can be carried out with any editor of your choice. It is also possible to use the .configure script, which can be found in the sources of the emulator. In that case, however, the file will not contain all the comments which extensively describe the possible options in the sample file. (Wait)

Now you can attempt to start the DOS emulator for the first time with the DOS diskette. No additional partitions, hard disks, or partitions mounted under Linux are as yet available. Also, it is not possible to access printers, hardware extensions or networks.

+- In the next step, you can provide access to the normal DOS partitions. The most popular way to do this is to use the redirector LREDIR.EXE or the driver EMFS.SYS. Both alternatives have the same functionality, drives can be assigned both in the file CONFIG.SYS and, later on, in the file AUTOEXEC.BAT or from the command line. For DOS programs, the drive behaves as if it were a network drive.

The call of the driver EMFS.SYS has the syntax DEVICE=EMFS.SYS Linux path [r]. This assigns the specified path under Linux to the next available drive letter. If, in addition, the parameter r is specified, the drive is write-protected.

```
DEVICE:A=\EMFS.SYS /mount/dos/c
DEVICE:A=\EMFS.SYS / r
```

The LREDIR.EXE serves the same purpose and can also be used from the command line. The following commands would yield the same result as above example:

```
A:LREDIR C: LINUX\MOUNT\DOS\nA:LREDIR D: LINUX\
```

Drive assignments can also be deleted by entering the command LREDIR del drive. The LREDIR command without parameters displays an overview of the drive assignments.
