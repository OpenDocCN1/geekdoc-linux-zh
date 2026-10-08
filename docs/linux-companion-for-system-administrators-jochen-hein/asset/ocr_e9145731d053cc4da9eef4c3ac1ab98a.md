# THE BIOS EMULATOR DOSemu 351

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
|---|---|
| --enable-novm8plus | The new variation for switching into vm86 mode is not used |
| --with-x=[yes|no] | With/without X support |
| --enable-nomitshm | Do not employ shared memory during X access |
| --enable-debugbug | Activate debugging |
| --enable-nosbem | Do not activate Soundblaster emulation |
| --enable-linkstatic | Link statically |
| --enable-runroot | Installation as setuid program |

Table 12.1 Options for the DOSemu configure script.

Any further configuration of the emulator can be carried out by means of the configuration file /etc/dosemu.conf or ~/.dosrc, so that it is not necessary to make changes to the Makefile file.

# 12.1.2 Configure the emulator

After installation, only the configuration files for the emulator need to be adapted. First of all, the names of all users who are allowed to start the DOS emulator must be registered in the file /etc/dosemu.users. This allows use of the emulator to be restricted to 'trustworthy' users. For many functions, such as graphical output or access to ports, it is necessary to start the emulator with