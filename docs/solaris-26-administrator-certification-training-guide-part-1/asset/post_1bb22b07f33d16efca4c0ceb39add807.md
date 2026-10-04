
3. In the Serial Ports window, select the port that will be used with a modem, as shown in Figure 12-2.

### Figure 12-2
The Serial Ports window.

![](img/85737305a4c9aeecbcadd9986d604c02_229_0.png)

4. Choose Edit, Modify, as shown in Figure 12-3. The Modify Serial Port window appears.

### Figure 12-3
The Serial Ports Edit menu.

![](img/85737305a4c9aeecbcadd9986d604c02_229_1.png)

The Modify Serial Port window appears in the Basic Detail mode. To enter additional details, select the More or Expert Detail mode.

5. From the drop-down Template list, choose the modem configuration template that meets—or most closely matches—your modem service (see Figure 12-4).

### Figure 12-4
The Modify Serial Port Template list.

![](img/85737305a4c9aeecbcadd9986d604c02_230_0.png)

A description of each modem selection can be found in Table 12-1.

### Table 12-1 The Modem Template
| Modem Configuration | Description |
|---|---|
| Dial In Only | Users can dial in to the modem but cannot dial out. |
| Dial Out Only | Users can dial out from the modem but cannot dial in. |
| Bidirectional | Users can dial either in or out from the modem. |

6. Select the correct baud rate from the Baud Rate drop-down list, as shown in Figure 12-5.

### Figure 12-5
The Baud Rate drop-down list.

![](img/85737305a4c9aeecbcadd9986d604c02_230_1.png)

Figure 12-6 shows a completed Modify Serial Port window. The Expert detail mode was selected to show all of the options that can be configured.

### Figure 12-6
Completed Modify Serial Port window.

![](img/85737305a4c9aeecbcadd9986d604c02_231_0.png)

Table 12-2 describes each configurable option shown in Figure 12-6.

### Table 12-2 Modify Serial Port Window Items
| Item | Description |
|---|---|
| Port | Lists the port or ports you selected from the Serial Ports main window. |
| Service | Specifies that the service for the port is turned on (enabled). |
| Baud Rate | Specifies the line speed used to communicate with the terminal. The line speed represents an entry in the /etc/ttydefs file. |
| Terminal Type | Shows the abbreviation for the type of terminal—for example, ansi or vt100. Similar abbreviations are found in /etc/termcap. This value is set in the $TERM environment variable. |
| Option: Initialize Only | Specifies that the port software is initialized but not configured. |
| Option: Bidirectional | Specifies that the port line is used in both directions. |
| Option: Software Carrier | Specifies that the software carrier detection feature is used. If the option is not checked, the hardware carrier detection signal is used. |
| Login Prompt | Shows the prompt displayed to a user after a connection is made. |
| Comment | Shows the comment field for the service. |
| Service Tag | Lists the service tag associated with this port—typically an entry in the /dev/term directory. |

### Table 12-2 Modify Serial Port Window Items (continued)
| Item | Description |
|---|---|
| Port Monitor Tag | Specifies the name of the port monitor to be used for this port. The default monitor is typically correct. |
| Create utmp Entry | Specifies that a utmp entry is created in the accounting files upon login. |
| Connect on Carrier | Specifies that a port's associated service is invoked immediately when a connect indication is received. |
| Service | Shows the program that is run upon connection. |
| Streams Modules | Shows the streams modules that are pushed before the service is invoked. |
| Timeout (secs) | Specifies the number of seconds before a port is closed if the open process on the port succeeds and no input data is received. |

7. Click OK to configure the port.

8. Use the pmadm command to verify the modem service has been configured for use.
To do so, type

```
pmadm -l -s ttya
```

The serial port is now configured and ready for use.

## Service Access Facility (SAF)

The SAF is the tool used for administering terminals, modems, and other network devices. The SAF is an open-systems solution that controls access to system and network resources through tty devices and local-area networks (LANs). SAF is not a program; it is a hierarchy of background processes and administrative commands that include sacadm, pmadm, ttyadm, and nisadmin. See Table 12-3 for a description of these commands.

### Table 12-3 SAF Commands
| Command | Description |
|---|---|
| sacadm | Used to add, delete, enable, disable, start, and stop port monitors. |
| pmadm | Configures port monitor services and the associated processes for individual ports. |
| ttyadm | Formats input to pmadm for serial ports. |
| sttydefs | Creates and modifies entries in the /etc/sttydefs file to describe terminal line characteristics. |
| nisadmin | Formats input to pmadm for remote printing. |

In particular, SAF enables you to

- Set up ttymon and listen port monitors (using the sacadm command)
- Set up ttymon port monitor services (using the pmadm and ttyadm commands)
- Set up listen port monitor services (using the pmadm and nisadmin commands)
- Troubleshoot tty devices
- Troubleshoot incoming network requests for printing service
- Troubleshoot the Service Access Controller (using the sacadm command)

The configuration files associated with SAF are described in Table 12-4.

### Table 12-4 Files Associated with SAF
| File | Description |
|---|---|
| /etc/saf/_sysconfig | Per system configuration script |
| /etc/saf/_sactab | SAC's administrative file; contains configuration data for the port monitors that the SAC controls |
| /etc/saf/pmtag | Home directory for port monitor pmtag |
| /etc/saf/pmtag/_config | Per-port monitor configuration script for port monitor pmtag if it exists |
| /etc/saf/pmtag/_pmtab | Port monitor pmtag's administrative file; contains port monitor-specific configuration data for the services pmtag provides |
| /etc/saf/pmtag/svctag | Per-service configuration script for service svctag |
| /var/saf/log | SAC's log file |
| /var/saf/pmtag | Directory for files created by pmtag, such as log files |

### sacadm
Use the sacadm command to add, list, remove, kill, start, enable, or disable a ttymon or listen port monitor. You must be logged in as superuser to use this command. For example, the command syntax used to add a ttymon port monitor is

```
sacadm -a -p mbmon -t ttymon -c /usr/lib/saf/ttymon -v 'ttyadm -V' -y "TTY Ports a & b"
```

Notice the use of the ttyadm command.

To view the newly added port monitor, type:

```
sacadm -l -p mbmon
```

The system responds with:

```
PMTAG   PMTYPE   FLGS   RCNT   STATUS   COMMAND
mbmon   ttymon   -      0      STARTING /usr/lib/saf/ttymon #TTY Ports a & b
```

The sacadm command options used for adding and viewing port monitors are listed in Table 12-5.

### Table 12-5 sacadm Command Options
| Command Option | Description |
|---|---|
| -a | Adds port monitor option |
| -c | Defines the command string used to start the port monitor |
| -k | Kills port monitor status option |
| -l | Lists port monitor status option |
| -p | Specifies the pmtag mbmon as the port monitor tag |
| -r | Removes port monitor status option |
| -s | Starts port monitor status option |
| -t | Specifies the port monitor type as ttymon |
| -v | Specifies the version number of the port monitor |
| -y | Defines a comment to describe this instance of the port monitor |

To kill a ttymon port monitor, type

```
sacadm -k -p mbmon
```

To restart a port monitor that has been killed, type

```
sacadm -s -p mbmon
```

To remove a port monitor, type

```
sacadm -r -p mbmon
```

### pmadm
The Port Monitor Service Administrator (pmadm) command enables you to administer port monitors' services. Use pmadm to add services, list the services of one or more ports associated with a port monitor, and enable or disable a service. An example would be a terminal service. You can also install or replace per-service configuration scripts or print information about a service.

When you use the pmadm command to administer a service, you specify a particular port monitor via the pm tag argument and a particular port via the svctag argument. For each port monitor type, the SAF requires a specialized command to format port monitor-specific configuration data. This data is used by the pmadm command.

To add a standard terminal service to the mbmon port monitor, type

```
pmadm -a -p mbmon -s a -i root -v 'ttyadm -V' -m '"ttyadm -i 'Terminal disabled' -l \ contty -m ldterm,ttcompat -S y -d /dev/term/a -s /usr/bin/login"'
```

Options used in the pmadm command are described in Table 12-6. Note that the above pmadm command contains an embedded ttyadm command.

### Table 12-6 pmadm Command Options
| Command Option | Description |
|---|---|
| -a | Adds port monitor status option |
| -d | Disables the port monitor service |
| -e | Enables the port monitor service |
| -l | Lists the port monitor service information |
| -p | Specifies the pm tag mbmon as the port monitor tag |
| -s | Specifies the svctag a as the port monitor service tag |
| -i | Specifies the identity to be assigned to svctag when it runs |
| -v | Specifies the version number of the port monitor |
| -m | Specifies the ttymon-specific configuration data formatted by ttyadm |

The next example uses the pmadm command to list the status of a TTY port, or all the ports associated with a port monitor. Type

```
pmadm -l -p mbmon
```

The system outputs the following information:

```
PMTAG PMTYPE SVCTAG FLAGS ID <PMSPECIFIC>
mbmon ttymon a . root /dev/term/a - - /usr/bin/login \
- contty ldterm,ttcompat login: Terminal disabled - y #Comment
```
