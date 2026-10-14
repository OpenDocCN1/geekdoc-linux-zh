| Symbol | Meaning |
|---|---|
| (==) | Defaults of the X server |
| (--) | Values taken from the system by automatic hardware detection. |
| (*) | Settings fixed in the configuration file. |
| (++) | Parameters entered at the command line. |
| (!!) | Here, the X server tells you in detail what it “is doing”. |
| (II) | Version numbers of X server modules, etc., are usually recorded as “informational messages”. |
| (WW) | Warnings: here the X server tells you why it is not carrying out certain actions specified in the configuration file or that should be activated by default. |
| (EE) | Error! These messages cancel the start procedure or crash the X server. Look out for lines in the log file starting with (EE) if the X server does not start. You can remedy most errors yourself by evaluating these messages. |

*Table 7.1: Message Types in the X Server Log File*

This provides the following information:

This is an XFree86 X server in version 4.0 compatible with X11R6.4 “vendor release 6.4.0”. The release date is 8th March, 2000. The line Operating System: Linux 2.2.13 i686 [ELF] SuSE refers to the system on which the X server was compiled. The kernel version and CPU definition can thus be different from your own system.

After these version messages, the first login entries appear that the X server creates when it starts. First of all, is this the correct log file? Next to Time:, the time when the log file was created is specified. Sometimes you might be searching in the wrong log file.

The same thing is valid for the configuration file. If you did not specify a different file at the command line, this will always be /etc/X11/XF86Config on a normal SuSE Linux system.

The following table 7.1 explains the meaning of the two bracket characters at the beginning of other lines:

If something unexpected happens when starting SaX2 or during the configuration steps, all errors and steps concerning SaX2 are logged in the file /var/log/SaX.log. X server errors are logged, as described above, in the file /var/log/XFree86.0.log. By means of these files, find clues on how to proceed.