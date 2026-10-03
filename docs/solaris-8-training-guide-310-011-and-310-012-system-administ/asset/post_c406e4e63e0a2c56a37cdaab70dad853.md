
Type eject-floppy to remove the disk.

Table 2.14 describes other OpenBoot commands that you can use to gather information about the system.

## TABLE 2.14
### SYSTEM INFORMATION COMMANDS

| Command | Description |
|---|---|
| banner | Displays the power-on banner. |
| show-sbus | Displays a list of installed and probed SBus devices. |
| .enet-addr | Displays the current Ethernet address. |
| .idprom | Displays ID PROM contents, formatted. |
| .traps | Displays a list of SPARC trap types. |
| .version | Displays the version and date of the startup PROM. |
| .speed | Displays CPU and bus speeds. |
| show-devs | Displays all installed and probed devices. |

The following example uses the banner command to display the CPU type, the installed RAM, the Ethernet address, the hostid, and the version and date of the startup PROM:

```
ok banner
```

The system responds with this:

```
Sun Ultra 5/10 UPA/PCI (UltraSPARC-IIIi 270MHz), No Keyboard
OpenBoot 3.15, 128 MB memory installed, Serial #10642306.
Ethernet address 8:0:20:a2:63:82, Host ID: 80a26382.
```

The next example uses the .version command to display the OpenBoot version and date of the startup PROM.

Type the following:

```
ok .version
```

The system responds with this:

```
Release 3.15 Version 2 created 1998/11/10 10:35
OBP 3.15.2 1998/11/10 10:35
POST 2.3.1 1998/08/07 16:33
```

> NOTE For Solaris 8 to work properly, your PROM release must be version 1.1 or higher. Use the banner command to find out the PROM release for your system.

The next example shows how to use the .enet-addr command to display the Ethernet address.

Type the following:

```
ok .enet-addr
```

The system responds with this:

```
8:0:20:1a:c7:e3
```

To display the CPU information, type

```
.speed
```

The system responds with this:

```
CPU  Speed : 270.00MHz
UPA  Speed : 090.00MHz
PCI  Bus A : 33MHz
PCI  Bus B : 33MHz
```

## Input and Output Control

The console is used as the primary means of communication between OpenBoot and the user. The console consists of an input device used for receiving information supplied by the user and an output device used for sending information to the user. Typically, the console is either the combination of a text/graphics display device and a keyboard or an ASCII terminal connected to a serial port.

The configuration variables relating to the control of the console are listed in Table 2.15.

## TABLE 2.15
### Console Configuration Variables

| Variable | Description |
|---|---|
| input-device | Console input device (usually keyboard, ttya, or ttyb). |
| output-device | Console output device (usually screen, ttya, or ttyb). |
| screen-#columns | Number of onscreen columns (the default is 80 characters per line). |
| screen-#rows | Number of onscreen rows (the default is 34 lines). |

You can use these variables to assign the console’s power-on defaults. These values do not take effect until after the next power cycle or system reset.

If you select keyboard for input-device and the device is not plugged in, input is accepted from the ttya port as a fallback device. If the system is powered on and the keyboard is not detected, the system will look to ttya—the serial port—for the system console and will use this port for all input and output.

The communication parameters on the serial port can be defined by setting the configuration variables for that port. These variables are shown in Table 2.16.

## TABLE 2.16
### Port Configuration Variables

| Variable | Current Value | Default Value |
|---|---|---|
| ttyb-rts-dtr-off | false | false |
| ttyb-ignore-cd | true | true |
| ttya-rts-dtr-off | false | false |
| ttya-ignore-cd | true | true |
| ttyb-mode | 9600,8,n,1,- | 9600,8,n,1,- |
| ttya-mode | 9600,8,n,1,- | 9600,8,n,1,- |

Following are the values for ttya-mode from left to right:

- Baud rate: 110, 300, 1200, 4800, 9600, 19200
- Data bits: 5, 6, 7, 8
- Parity: n (none), e (even), o (odd), m (mark), s (space)
- Stop bits: 1, 1.5, 2
- Handshake: - (none), h (hardware: rts/cts), s (software: xon/xoff)

## BOOT

The primary function of the OpenBoot firmware is to start up the system. Starting up is the process of loading and executing a stand-alone program. An example of a stand-alone program is the operating system or the diagnostic monitor. In this discussion, the stand-alone program is the operating system kernel. After the kernel is loaded, it starts the UNIX system, mounts the necessary file systems, and runs /sbin/init to bring the system to the “initdefault” state specified in /etc/inittab. This process was discussed in Chapter 1.

Starting up can be initiated either automatically or by typing a command at the user interface. It is commonly referred to as the bootstrap procedure. On most SPARC-based systems, the bootstrap procedure consists of the following basic phases:

- 1. The system hardware is powered on.
- 2. The system firmware (the PROM) executes a POST. (The form and scope of these tests depends on the version of the firmware in your system.)
- 3. After the tests have been completed successfully, the firmware attempts to autoboot if the appropriate OpenBoot configuration variable (auto-boot?) has been set.

The OpenBoot startup process is shown here:

```
Sun Ultra 5/10 UPA/PCI (UltraSPARC-IIIi 270MHz), No Keyboard
OpenBoot 3.15, 128 MB memory installed, Serial #10642306.
Ethernet address 8:0:20:a2:63:82, Host ID: 80a26382.
Rebooting with command: boot
Boot device: disk:a  File and args:
SunOS Release 5.8 Version Generic_108621-04 64-bit
Copyright 1983-2000 Sun Microsystems, Inc.  All rights reserved.
configuring IPv4 interfaces: hme0.
configuring IPv6 interfaces: hme0.
Hostname: ultra
metainit: unknown: there are no existing databases
The system is coming up.  Please wait.
checking ufs filesystems
/dev/rdsk/c0t0d0s5: is clean.
/dev/rdsk/c0t0d0s7: is clean.
/dev/rdsk/c0t0d0s6: is clean.
Starting IPv6 neighbor discovery. Setting default IPv6 interface for
multicast: add net ff00::/8: gateway fe80::a0:20ff:fea2:6382
starting rpc services: rpcbind done.
Setting default IPv4 interface for multicast: add net 224.0/4: gateway unknown
syslog service starting.
syslogd: line 24: WARNING:loghost could not be resolved
Print services started.
volume management starting.
Mar 23 13:19:33 unknown snmpdx:
The system is ready.
ultra console login:
```

The startup process is controlled by a number of configuration variables. The ones that affect the startup process are described in Table 2.17.

## TABLE 2.17
### Boot Configuration Variables

| Variable | Description |
|---|---|
| auto-boot? | Controls whether the system automatically starts up after a system reset or when the power is turned on. The default for this variable is true. When the system is powered on, the system automatically starts up to the default run level. |
| boot-command | Specifies the command to be executed when auto-boot? is true. The default value of boot-command is boot with no command-line arguments. |
| diag-switch? | If the value is true, runs in the diagnostic mode. This variable is false by default. |
| boot-device | Contains the name of the default startup device that is used when OpenBoot is not in diagnostic mode. |
| boot-file | Contains the default startup arguments that are used when OpenBoot is not in diagnostic mode. The default is no arguments. (See Table 2.18 for details of when this variable is used.) |
| diag-device | Contains the name of the default diagnostic mode startup device. The default is net. (See Table 2.18 for details of when this variable is used.) |

continues

## TABLE 2.17 continued
### Boot Configuration Variables

| Variable | Description |
|---|---|
| diag-file | Contains the default diagnostic mode startup arguments. The default is no arguments. (See Table 2.18 for details of when this variable is used.) |

Typically, auto-boot? will be true, boot-command will be boot, and OpenBoot will not be in diagnostic mode. Consequently, the system will automatically load and execute the program, and arguments described by boot-file from the device described by boot-device when the system is first turned on or following a system reset. The boot command and its options are described in Table 2.18.

boot has the following syntax:

```
boot [OBP name] [filename] [options] [flags]
```

[OBP name], [filename], [options], and [flags] are optional.

## TABLE 2.18
### boot Command

| Option | Description |
|---|---|
| OBP name | Specifies the OpenBoot PROM designations. For example, on Desktop SPARC-based systems, the designation /sbus/esp@0,800000/sd@3,0:a indicates a SCSI disk (sd) at target 3, lun0 on the SCSI bus, with the esp host adapter plugged into slot 0. This OBP name can be a devalias, such as disk0 (floppy 3 1/2-inch diskette drive), net (Ethernet), or tape (SCSI tape). If OBP name is not specified and diagnostic-mode? returns true, boot uses the device specified by the diag-device configuration variable. |
| filename | The name of the stand-alone program to be started up (for example, kernel/unix). The default is to start up /platform/platform-name/kernel/unix from the root partition. If specified, filename is relative to the root of the selected device and partition. If not, the boot program uses the value of the boot-file or diag-file based on the diag-switch? parameter. |
