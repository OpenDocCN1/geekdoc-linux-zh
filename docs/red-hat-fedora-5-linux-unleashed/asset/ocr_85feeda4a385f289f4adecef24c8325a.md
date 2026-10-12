```
/etc/sysconfig/system-config-users
/etc/sysconfig/tux
/etc/sysconfig/vncservers
/etc/sysconfig/xinetd
```

10 directories, 94 files

For brevity, not all directories and files are discussed here. /etc/sysconfig contains many different hardware and software settings critical to the operation of your Fedora system. Knowing the location and contents of these files can be helpful if you need to trouble- shoot new hardware configurations.

The settings in various files under /etc/sysconfig (such as keyboard, mouse, sound, and so on) are usually created automatically by a related Fedora graphical or console-based configuration utility.

These contents might dynamically change if you use the kudzu hardware configuration service. The kudzu service also prompts you at boot time to remove, configure, or ignore a related setting if kudzu detects new or different hardware (such as a new USB keyboard, network card, or monitor). kudzu creates a file called hwconf that contains a hardware profile of your PC’s current state. Note that if kudzu is not enabled or running, you can use device-specific configuration utilities such as system-config-keyboard, or you can manually edit configuration files.

Information about the type of pointing device attached to the PC, for example, is contained in the file /etc/sysconfig/mouse:

```
MOUSETYPE="ps/2"
XMOUSETYPE="PS/2"
FULLNAME="Generic 3 Button Mouse (PS/2)"
XEMU3=no
```

If a different mouse, say a three-button USB device, is attached to the computer, you can edit this information to reflect the hardware change:

```
MOUSETYPE="ps/2"
XMOUSETYPE="IMPS/2"
FULLNAME="Generic 3 Button Mouse (USB)"
XEMU3=no
```

> **CAUTION**
> 
> If you are new to Linux, the system-config-mouse client is the best tool to use to configure a new mouse. You should manually edit system hardware configuration files used by graphical management clients only as a last resort.