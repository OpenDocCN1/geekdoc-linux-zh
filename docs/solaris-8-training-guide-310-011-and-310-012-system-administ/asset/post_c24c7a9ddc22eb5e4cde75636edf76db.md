
The following example creates a device alias named disk3, which represents a SCSI disk with a target ID of 3 on a SPARCstation10 system:

```
devalias disk3 /iommu/sbus/espdma@f,400000/esp@f,800000/sd@3,0
```

To confirm the alias, type devalias, and the system will print all the aliases:

```
ok devalias
screen          /iommu@f,e0000000/sbus@f,e0001000/cgsix@2,0
disk5           /iommu/sbus/espdma@f,400000/esp@f,800000/sd@0,0
floppy          /obio/SUNW,fdtwo
scsi            /iommu/sbus/espdma@f,400000/esp@f,800000
net-aui         /iommu/sbus/ledma@f,400010:aui/le@f,c00000
net-tpe         /iommu/sbus/ledma@f,400010:tpe/le@f,c00000
net             /iommu/sbus/ledma@f,400010/le@f,c00000
disk            /iommu/sbus/espdma@f,400000/esp@f,800000/sd@3,0
cdrom           /iommu/sbus/espdma@f,400000/esp@f,800000/sd@6,0:d
tape            /iommu/sbus/espdma@f,400000/esp@f,800000/st@4,0
tape0           /iommu/sbus/espdma@f,400000/esp@f,800000/st@4,0
tape1           /iommu/sbus/espdma@f,400000/esp@f,800000/st@5,0
disk3           /iommu/sbus/espdma@f,400000/esp@f,800000/sd@3,0
disk2           /iommu/sbus/espdma@f,400000/esp@f,800000/sd@2,0
disk1           /iommu/sbus/espdma@f,400000/esp@f,800000/sd@1,0
disk0           /iommu/sbus/espdma@f,400000/esp@f,800000/sd@3,0
ttyb            /obio/zs@0,100000:b
ttya            /obio/zs@0,100000:a
keyboard!       /obio/zs@0,0:forcemode
keyboard        /obio/zs@0,0
```

User-defined aliases are lost after a system reset or power cycle unless you create a permanent alias. If you want to create permanent aliases, you can either manually store the devalias command in a portion of non-volatile RAM (NVRAM) called nvramrc, or use the nvalias and nvunalias commands. The following section describes how to configure permanent settings in the NVRAM on a Sun system.

## OpenBoot Non-Volatile RAM (NVRAM)

System configuration variables are stored in the system NVRAM. These OpenBoot variables determine the startup machine configuration and related communication characteristics. You can modify the values of the configuration variables, and any changes you make remain in effect, even after a power cycle. Configuration variables should be adjusted cautiously, however.

Table 2.7 describes OpenBoot's NVRAM configuration variables, their default values, and their functions.

TABLE 2.7
NVRAM VARIABLES

| Variable | Default | Description |
|---|---|---|
| auto-boot? | true | If true, start up automatically after power on or reset. |
| boot-command | boot | Command that is executed if auto-boot? is true. |
| boot-device | disk or net | Device from which to start up. |
| boot-file | Empty string | Arguments passed to the started program. |
| diag-device | net | Diagnostic startup source device. |
| diag-file | Empty string | Arguments passed to the startup program in diagnostic mode. |
| diag-switch? | false | If true, run in diagnostic mode. |
| fcode-debug? | false | If true, include name fields for plug-in device FCodes. |
| input-device | keyboard | Console input device (usually keyboard, ttya, or ttyb). |
| nvramrc | Empty | Contents of NVRAMRC. |
| oem-banner | Empty string | Custom OEM banner (enabled by oem-banner? true). |
| oem-banner? | false | If true, use custom OEM banner. |
| oem-logo | No default | Byte array custom OEM logo (enabled by oem-logo? true). Displayed in hexadecimal. |
| oem-logo? | false | If true, use custom OEM logo; otherwise, use Sun logo. |
| output-device | screen | Console output device (usually screen, ttya, or ttyb). |
| sbus-probe-list | 0123 | Which SBus slots to probe and in what order. |
| screen-#columns | 80 | Number of onscreen columns (characters/line). |
| screen-#rows | 34 | Number of onscreen rows (lines). |
| security-#badlogins | No default | Number of incorrect security password attempts. |
| security-mode | none | Firmware security level (options: none, command, or full). |
| security-password | No default | Firmware security password (never displayed). |
| use-nvramrc? | false | If true, execute commands in NVRAMRC during system startup. |

NOTE
Older SPARC systems, because they use older versions of OpenBoot, might use different defaults or different configuration variables. As mentioned earlier, this text describes OpenBoot version 3.

The NVRAM configuration variables can be viewed and changed using the commands listed in Table 2.8.

## TABLE 2.8

## VIEWING OR MODIFYING CONFIGURATION VARIABLES

| Command | Description |
|---|---|
| password | Sets the security password. |
| printenv | Displays the current value and the default value for each variable. To show the current value of a named variable, type printenv <parameter name>. |
| setenv variable value | Sets the variable to the given decimal or text value. Changes are permanent, but they often take effect only after a reset. |
| set-default variable | Resets the value of the variable to the factory default. |
| set-defaults | Resets variable values to the factory defaults. |

The following examples illustrate the use of the commands described in Table 2.8.

All commands are entered at the ok OpenBoot prompt.

```
ok printenv
```

The system responds with this:

| Variable Name | Value | Default Value |
|---|---|---|
| tpe-link-test? | true | true |
| scsi-initiator-id | 7 | 7 |
| keyboard-click? | false | false |
| keymap |  |  |
| ttyb-rts-dtr-off | false | false |
| ttyb-ignore-cd | true | true |
| ttya-rts-dtr-off | false | false |
| ttya-ignore-cd | true | true |
| ttyb-mode | 9600,8,n,1,- | 9600,8,n,1,- |
| ttya-mode | 9600,8,n,1,- | 9600,8,n,1,- |
| pcia-probe-list | 1,2,3,4 | 1,2,3,4 |
| pcib-probe-list | 1,2,3 | 1,2,3 |
| mfg-mode | off | off |
| diag-level | max | max |
| #power-cycles | 89 |  |
| system-board-serial# |  |  |
| system-board-date |  |  |
| fcode-debug? | false | false |
| output-device | screen | screen |
| input-device | keyboard | keyboard |
| load-base | 16384 | 16384 |
| boot-command | boot | boot |
| auto-boot? | false | true |
| watchdog-reboot? | false | false |
| diag-file |  |  |
| diag-device | net | net |
| boot-file |  |  |
| boot-device | disk:a disk net | disk net |
| local-mac-address? | false | false |
| ansi-terminal? | true | true |

NOTE
Depending on the version of OpenBoot you have on your system, the printenv command might show slightly different results. For this example, I used a system running OpenBoot version 3.15.

```
screen-#columns      80                  80
screen-#rows         34                  34
silent-mode?         false               false
use-nvramrc?         false               false
nvramrc              .
security-mode        none
security-password
security-#badlogins  0
oem-logo
oem-logo?            false               false
oem-banner
oem-banner?          false               false
hardware-revision
last-hardware-update
diag-switch?         false               false
```

To set the auto-boot? variable to false, type the following:

```
ok setenv auto-boot? false
```

Verify the setting by typing the following:

```
ok printenv auto-boot?
```

The system will respond with this:

```
auto-boot?   false   true
```

To reset the variable to its default setting, type the following:

```
ok set-default auto-boot?
```

Verify the setting by typing the following:

```
ok printenv auto-boot?
```

The system will respond with this:

```
auto-boot?   true   true
```

To reset all variables to their default settings, type the following:

```
ok set-defaults
```

It’s also possible to set these variables from the UNIX command line by issuing the eeprom command. You must be logged-in as root to issue these commands, and although anyone can view a parameter, only root can change the value of a parameter. For example, to set the auto-boot? variable to true, type the following at the UNIX prompt:

```
eeprom auto-boot?=true
```
