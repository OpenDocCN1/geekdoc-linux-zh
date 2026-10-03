# TABLE 2.17 continued

# Boot Configuration Variables

| Variable | Description |
|---|---|
| diag-file | Contains the default diagnostic mode startup arguments. The default is no arguments. (See Table 2.18 for details of when this variable is used.) |

Typically, auto-boot? will be true, boot-command will be boot, and OpenBoot will not be in diagnostic mode. Consequently, the system will automatically load and execute the program, and arguments described by boot-file from the device described by boot-device when the system is first turned on or following a system reset. The boot command and its options are described in Table 2.18.

boot has the following syntax:

```
boot [OBP name] [filename] [options] [flags]
```

[OBP name], [filename], [options], and [flags] are optional.

# TABLE 2.18

# boot Command

| Option | Description |
|---|---|
| OBP name | Specifies the OpenBoot PROM designations. For example, on Desktop SPARC-based systems, the designation /sbus/esp@0,800000/sd@3,0:a indicates a SCSI disk (sd) at target 3, lun0 on the SCSI bus, with the esp host adapter plugged into slot 0. This OBP name can be a devalias, such as disk0 (floppy 3 1/2-inch diskette drive), net (Ethernet), or tape (SCSI tape). If OBP name is not specified and diagnostic-mode? returns true, boot uses the device specified by the diag-device configuration variable. |
| filename | The name of the stand-alone program to be started up (for example, kernel/unix). The default is to start up /platform/platform-name/kernel/unix from the root partition. If specified, filename is relative to the root of the selected device and partition. If not, the boot program uses the value of the boot-file or diag-file based on the diag-switch? parameter. |