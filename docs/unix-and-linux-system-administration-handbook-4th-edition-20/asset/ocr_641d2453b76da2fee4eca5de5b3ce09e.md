# The RS-232C standard

communicate with legacy systems. There are even cases in which you might run into an actual hardwired terminal, such as on a manufacturing floor.

This chapter describes how to connect and use RS-232-based serial devices in the modern world. The first few sections address serial hardware and cabling iterations. Then, starting on page 1171, we talk about the software infrastructure that supports both hardwired terminals and the pseudoterminals that emulate them. Finally, we cover the use of a UNIX or Linux system to communicate with the serial consoles of other devices.

# 31.1 The RS-232C STANDARD

Most-speed serial ports conform to some variant of the RS-232C standard. This standard specifies the electrical characteristics and meaning of each signal wire, as well as the pin assignments on the traditional 25-pin (DB-25p) serial connector in Exhibit A.

# Exhibit A A male DB-25 connector

| Connector | Pin numbers |
| --- | --- |
| | 1 ---> 13 |
| | 14 ---> 25 |

![](bbox=[0.26, 0.483, 0.893, 0.573])

Full RS-232C is never used in real-world situations since it defines numerous signals that are unnecessary for basic communication. DB-25 connectors are also inconveniently large. As a result, 9-pin DB-9 connectors are commonly used instead of the original 25-pin flavor. In cases where structured cabling is used, RJ-45 connectors are also a convenient alternative. Both of these are described in the section titled Alternative connectors starting on page 1165.

Exhibit A shows a male DB-25. As with all the pin numbers on a female connector are a mirror image on a male connector so that numbered pins match. The diagram is drawn from the orientation shown, as if you were facing the end of the cable, about to plug the connector into your forehead.

Note that in Exhibit A, only seven pins are actually installed, which is typical. The RS-232 signals and their pin assignments on a full-size DB-25 connector are

+   1. To technically correct, this standard should now be referred to as EIA-232-E. However, no one will have the slightest idea what you are talking about.