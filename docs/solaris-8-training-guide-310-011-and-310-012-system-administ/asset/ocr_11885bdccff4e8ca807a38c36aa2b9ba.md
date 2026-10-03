Any user can view the OpenBoot configuration variables from a UNIX prompt by typing the following:

```
/usr/sbin/eeprom
```

For example, to change the OpenBoot parameter security-password from the command line, you must be logged in as root and issue the following command:

```
example# eeprom security-password=
Changing PROM password:
New password:
Retype new password:
```

The security password you assign must be between zero and eight characters. Any characters after the eighth are ignored. You do not have to reset the system; the security feature takes effect as soon as you type the command.

With no parameters, the eeprom command will display all the OpenBoot configuration settings, similar to the OpenBoot printenv command.

The NVRAM commands listed in Table 2.9 can be used to modify devaliases so that they remain permanent, even after a restart.

# TABLE 2.9

# NVRAM Commands

| Command | Description |
|---|---|
| nvalias alias device-path | Stores the command devalias alias device-path in NVRAMRC. (The alias persists until the nvunalias or set-defaults commands are executed.) Turns on use-nvramrc? |
| nvunalias alias | Deletes the corresponding alias from NVRAMRC. |

For example, to permanently create a devalias named disk3, which will represent a SCSI disk with a target ID of 3 on a SPARCstation10 system, type the following:

```
nvalias disk3/iommu/sbus/espdma@f,400000/esp@f,800000/sd@3,0
```

> CAUTION
Setting the security mode and password can leave a system unable to boot if you forget the password. It is impossible to break in without sending the CPU to Sun to have the PROM reset. OpenBoot security is discussed more in the next section.

> NOTE
If you change an NVRAM setting on a SPARC system and the system will no longer start up, it is possible to reset the NVRAM variables to their default settings by holding down the Stop+N keys simultaneously while the machine is powering up. When issuing this command, hold down Stop+N immediately after turning on the power to the SPARC system; keep these keys pressed for a few seconds or until you see the banner (if the display is available). This is a good technique to force a system's NVRAM variables to a known condition.