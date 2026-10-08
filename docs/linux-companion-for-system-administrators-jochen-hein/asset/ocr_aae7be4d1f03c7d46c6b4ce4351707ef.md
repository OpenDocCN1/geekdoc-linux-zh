# THE BIOS EMULATOR DOSemu 355

begins with the keyword X. Extensive documentation of the possible settings can be found in the sample configuration.

+   Now, additional hardware can be configured, for example the mouse or the access to the serial interfaces. Extensively commented samples for all settings can be found in the configuration file.

# System security considerations

Since the emulator carries out many accesses closely related to the hardware, it is installed as a setuid program. Thus, many accesses are executed with privileges of the system administrator root. In a true, networked multi-user system, this is not looked upon kindly. In this case, one should consider whether direct hardware access can be completely prevented by means of an appropriate configuration of the emulator. This, however, would also provide access to the ports and make a direct emulation of the loudspeaker and representation of graphics on screen impossible.

For this reason, the configuration files provide the option of making special settings depending on the user name or the current computer. Thus it is possible for guest users to be allowed to use the emulator, but that the emulator does not provide all functions. Other, trustworthy users, on the other hand, may use all the emulator's possibilities. The sample configuration of DOSemu includes various examples.

# Error detection support

The emulator is able to output different items of information for debugging purposes. On the one hand, you can trigger the corresponding output by specifying the keyword debug in the configuration file. Another option is the specification as a parameter. In the following example, all messages are displayed and stored in the file dos.log. This file can be of great help for debugging the emulator or the configuration file. Generation of debug output can be toggled by means of the DOSDBG program even with the emulator running. These files can become shockingly huge in a very short time if you activate all output as in the following command.

```
(Linux):~$ dos -D+a -o dos.log
```