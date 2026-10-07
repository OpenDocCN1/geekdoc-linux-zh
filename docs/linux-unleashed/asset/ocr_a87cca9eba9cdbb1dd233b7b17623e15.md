# ## HDB UUCP Configuration

HDB UUCP is a more recent version of UUCP and its configuration files are different. In many ways, the HDB configuration is easier than Taylor UUCP's, although neither is difficult once you know the basic process.

The name of the local system is not set in the UUCP configuration files but by the Linux hostname itself. To set the system name use the hostname command.

The names of the remote systems are stored in the file `/usr/lib/uucp/Systems` (some older versions used the name `/usr/lib/uucp/L.sys`). There is a single line for each remote system that you will be connected to. The format of each line is as follows:

```
sitename schedule device_type speed phone login_script
```

*sitename* is the name of the remote machine, *schedule* is when it can be connected, *device_type* is the type of device to use to call the remote system, *speed* is the speed (or range of speeds) that can be used to connect, *phone* is the telephone number, and *login_script* is the script used when a connection is made (such as the chat script in Taylor UUCP). For example, to call the remote system arthur, the `/usr/lib/uucp/Systems` file will have a line like this:

```
arthur Any ACU 9600 555-1212 login: uucp password: secret1
```

The Any entry in the schedule field tells UUCP that it can call at any time. The ACU entry in the device field tells UUCP to use the ACU (automatic calling unit) defined in the `/usr/lib/uucp/Devices` file.

The `/usr/lib/uucp/Devices` file (or `/usr/lib/uucp/L.devices` file in some older versions) contains information about the devices that can be used to call the remote systems. The Devices file follows this syntax:

```
devicetype ttyline dialerline speed dialer [token Dialer ...]
```

*devicetype* is the name of the device (which should match the device name in the `/usr/lib/uucp/Systems` file), *ttyline* is the device driver to be used for the connecting port (usually a serial line, such as `/dev/tty2a` or `/dev/modem`), *dialerline* is an obsolete field left as a hyphen, *speed* is the speed range of the device, and *dialer* is the name of the file that tells UUCP how to use the device. A sample line for a Hayes 9600 baud modem used to connect on the second serial port of the system might have an entry in the `/usr/lib/uucp/Devices` file such as

```
ACU tty2A - 9600 dialHA96
```