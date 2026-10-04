
responsible for loading the UNIX kernel into memory and passing control of the system to the kernel. The kernel is a file named /kernel/unix, located on the bootable device.

The OpenBoot firmware was first introduced on the Sun SPARCstation 1. This chapter describes Version 2 of the firmware, which first appeared on the SPARCstation 2 system. Version 2 of the OpenBoot architecture provides a significant increase in functionality over the boot PROMs in earlier Sun systems. One notable feature of the OpenBoot firmware is a programmable user interface, based on the interactive programming language Forth. In Forth, sequences of user commands can be combined to form complete programs. This capability provides a powerful tool for debugging hardware and software.

You can enter the OpenBoot environment in the following ways:

- By halting the operating system with the various UNIX shutdown commands.
- By using the Stop-A key sequence from the keyboard (simultaneously press the Stop key and the A key).

> **CAUTION!** Using the Stop-A key sequence abruptly breaks execution of the operating system and should be used only as a last effort to restart the system.

- By resetting the power to the system.

> **NOTE.** If your system is configured to boot automatically, you can enter the OpenBoot environment by pressing Stop-A after the display console banner appears but before the system starts booting the operating system. This procedure is not the same as the method described above, in which the Stop-A sequence is pressed after the system has booted. If automatic booting is not enabled, the system enters the OpenBoot environment on its own instead of booting the operating system.

- When the system hardware detects an error from which it cannot recover. (The system halts and puts you at the OpenBoot prompt. This system failure is known as a Watchdog Reset.)

## OpenBoot Interface

The OpenBoot firmware provides a command line interface for the user at the system console, which has two modes: the Restricted Monitor and the Forth Monitor.

The Restricted Monitor provides a simple set of commands to initiate booting of the system, resume system execution, or enter the Forth Monitor. The Restricted Monitor is also used to implement system security.

The Restricted Monitor prompt is >. When you enter the Restricted Monitor, the following screen is displayed, showing the commands you can enter:

```
Type b (boot), c (continue), or n (new command mode) >
```

The Restricted Monitor commands are:

- `b specifiers` Boot the operating system.
- `c` Resume the execution of a halted program.
- `n` Enter the Forth Monitor (commonly referred to as "new command mode").

The Forth Monitor, the default mode in OpenBoot, is an interactive command interpreter that gives you access to an extensive set of functions for hardware and software diagnosis. These functions are available to anyone who has access to the system console.

The Forth Monitor prompt is ok. When you enter the Forth Monitor mode, the following screen is displayed:

```
Type help for more information ok
```

If you want to leave the Forth Monitor mode and get into the Restricted Monitor mode, type:

```
ok old-mode
```

**NOTE.** When the system is halted, the PROM monitor prompt is displayed. The type of prompt depends on your system type. Older Sun systems, such as the Sun4/mn series, use the greater than sign (>) as the PROM prompt. Newer Sun systems use ok as the PROM prompt but support the > prompt. To switch from the > prompt to the ok prompt on newer Sun systems, type n at the > prompt.

## How to Find the PROM Release for a System

For Solaris 2.6 to work properly, your PROM release must be revision 1.1 or higher. To get the PROM release on your system, type banner at the ok PROM prompt and press Enter. Hardware configuration information, including the release number of the PROM, is displayed:

```
ok banner
SPARCstation 2, Type 4 Keyboard
ROM Rev. 2.2, 16 MB memory installed, Serial #426751
Ethernet address 8:0:20:e:fd:7c HostID 55411df8
```

The OpenBoot PROM monitor supports three security modes (nonsecure, command secure, and fully secure) and an authentication password. Access to monitor commands is controlled by these security modes. In nonsecure mode, all monitor commands are allowed. In command secure mode, only the b (boot) command with no arguments and the c (continue) command with no arguments may be entered without supplying the authentication password. In fully secure mode, only the c (continue) command with no arguments may be entered without supplying the authentication password. Note that systems do not auto-reboot in fully secure mode. The authentication password must be entered before booting takes place.

## OpenBoot Parameters

The OpenBoot PROM supports several parameters, which are user-definable (superuser only). The following list provides a few common ones you should remember. The only time you should need to modify these parameters is if you want to boot from a SCSI disk other than target 3, in which case you might want to turn off automatic booting (auto-boot). Another reason you might want to change an OpenBoot parameter is for setting security. Don't change OpenBoot parameters unless absolutely necessary. Not all OpenBoot systems support all parameters, and defaults can vary, depending on the system and the PROM revision.

### Version 2 OpenBoot Parameters

Table 1-1 describes some of the OpenBoot parameters. For a more complete listing, refer to the OpenBoot Command Reference Manual for the version of OpenBoot on your system.

### Table 1-1 OpenBoot Parameters

| Parameter | Description |
|---|---|
| auto-boot? | If true, boots automatically after power-on or reset. Default=true. |
| boot-device | Device from which to boot. Defaults to disk. Note: Disk is an alias that can be user-defined. |
| input-device | Power-on input device (usually keyboard, ttya, or ttyb). Default=keyboard. |
| output-device | Power-on output device (usually screen, ttya, or ttyb). Default=screen. |
| security-#badlogins | Number of incorrect security password attempts. |
| security-mode | Firmware security level (options: none, command, or full). If set to command or full, system prompts for PROM security password. Default=none. |
| security-password | Firmware security password (never displayed). Can be set only when security-mode is set to command or full. |
| watchdog-reboot? | If true, reboots after watchdog reset. Default=false. |

The following example demonstrates the method for setting the auto-boot? parameter to false. At the ok prompt, type auto-boot?=false.

An OpenBoot parameter can also be changed from the UNIX command line by using the eeprom command without being at the openboot prompt. After a parameter is changed, it remains that way even after a reboot. To change the OpenBoot parameter security-password from the command line, use the following:

```
example# eeprom security-password=
Changing PROM password:
New password:
Retype new password:
```

**CAUTION!** Setting the security mode and password can leave a system unable to boot if you forget the password. There is no way to break in without sending the CPU to Sun to have the PROM reset.

## PROM Device Names, Addresses, and Arguments

Sun's firmware deals directly with hardware devices in the system. Each device has a unique name, representing the type of device and a path to that device's location in the hardware hierarchy or the system addressing structure. The following example shows a full device pathname:

/sbus1@f8000000/esp@,80000/sd@3,0:a

A full device pathname consists of information, or node names, separated by slashes (/). The root of the tree is the machine node, which is not named explicitly but is indicated by a leading slash (/). Each node name has the form

```
name@address:arguments
```

Table 1-2 describes the parameters in the node name.

### Table 1-2 Full Device Path Node Name Parameters

| Node Name Parameter | Description |
|---|---|
| name | A text string that, ideally, has some mnemonic value (for example, sd represents "SCSI disk"). Many names, especially names of plug-in modules, include the name or stock symbol of the device's manufacturer (for example, SUNW is the stock symbol for Sun Microsystems). |
| @ | Separates the name from the address parameter. |
| address | A text string representing an address, usually of the form hex_number,hex_number. (Numbers are given in hexadecimal format.) |
| : | Must precede the argument's parameter. |
| arguments | A text string whose format depends on the particular device. It can be used to pass information to the device's software. |
