remains that way even after a reboot. To change the OpenBoot parameter security-password from the command line, use the following:

```
example# eeprom security-password=
Changing PROM password:
New password:
Retype new password:
```

**CAUTION!** Setting the security mode and password can leave a system unable to boot if you forget the password. There is no way to break in without sending the CPU to Sun to have the PROM reset.

# PROM Device Names, Addresses, and Arguments

Sun's firmware deals directly with hardware devices in the system. Each device has a unique name, representing the type of device and a path to that device's location in the hardware hierarchy or the system addressing structure. The following example shows a full device pathname:

```
/sbus1@f8000000/esp@,80000/sd@3,0:a
```

A full device pathname consists of information, or node names, separated by slashes (/). The root of the tree is the machine node, which is not named explicitly but is indicated by a leading slash (/). Each node name has the form

```
name@address:arguments
```

Table 1-2 describes the parameters in the node name.

Table 1-2 Full Device Path Node Name Parameters

| Node Name Parameter | Description |
|---|---|
| name | A text string that, ideally, has some mnemonic value (for example, sd represents "SCSI disk"). Many names, especially names of plug-in modules, include the name or stock symbol of the device's manufacturer (for example, SUNW is the stock symbol for Sun Microsystems). |
| @ | Separates the name from the address parameter. |
| address | A text string representing an address, usually of the form hex_number,hex_number. (Numbers are given in hexadecimal format.) |
| : | Must precede the argument's parameter. |
| arguments | A text string whose format depends on the particular device. It can be used to pass information to the device's software. |