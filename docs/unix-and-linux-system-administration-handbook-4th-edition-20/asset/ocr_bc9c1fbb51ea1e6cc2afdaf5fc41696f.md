# Chapter 31 Serial Devices and Terminals

shown in Table 31.1. Only the shaded signals are used in practice (at least on computer systems); all others can be ignored.

# Table 31.1 RS-232 signals and pin assignments on a DB-25

| Pin | Function | Pin | Name | Function |
|---|---|---|---|---||
| 1 | FG | Frame ground | 14 | STD | Secondary TD |
| 2 | TD | Transmitted data | 15 | TC | Transmit clock |
| 3 | RD | Received data | 16 | SRD | Secondary RD |
| 4 | RTS | Request to send | 17 | RC | Receive clock |
| 5 | CTS | Clear to send | 18 | | Not assigned |
| 6 | DSR | Data ready | 19 | SRS | Secondary RTS |
| 7 | SG | Signal ground | 20 | DTR | Data quality detector |
| 8 | DCD | Data carrier detector | 21 | SQ | Signal quality |
| 9 | | Positive voltage | 22 | RI | Ring indicator |
| 10 | | Negative voltage | 23 | DRS | Data rate selector |
| 11 | | Not assigned | 24 | SCTE | Clock transmit external |
| 12 | SDCD | Secondary DCD | 25 | BUSY | Busy |
| 13 | SCTS | Secondary CTS | | |

Unlike connector standards such as USB and Ethernet RS-232 requires you to know what types of devices you are connecting. Two interface configurations exist: DTE (Data Terminal Equipment) and DCE (Data Communications Equipment). DTE and DCE share the same pinouts, but they specify different interpretations of the RS-232 signals.

Every device is configured as either DTE or DCE; a few devices support both, but not simultaneously. Computers, terminals, and printers are generally DTE, and most are DCE. DTE and DCE serial ports can communicate with each other in any combination, but different combinations require different cabling.

There is no sensible reason for both DTE and DCE to exist; all equipment could use the same wiring scheme. The existence of two conventions is merely one of the many pointless historical legacies of RS-232.

DTE and DCE can be confusing if you let yourself think the implications too much. When happens, just take a deep breath and reread these points:

+   - The RS-232 pinout for a given connector is always the same, regardless of whether the connector is male or female (matching pin numbers always mate) and regardless of whether the connector is a cable, a DTE device, or a DCE device.

+   - All RS-232 terminology is based on the model of a straight-through connection from a DTE device to a DCE device. By “straight through,” we mean that the DTE is connected to TD on the DCE end, and so on. Each pin connects to the same-numbered pin on the other end.