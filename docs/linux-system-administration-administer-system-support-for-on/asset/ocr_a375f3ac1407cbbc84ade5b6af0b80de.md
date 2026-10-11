# UPS Status

For UPS battery status, the `upsd` daemon is designed to monitor the UPS. There are some tools currently available at <http://sunsite.unc.edu/pub/Linux/system/ups> . There are a couple other monitoring utilities like Genpower that have automated shutdown and low battery detection. Table 10-3 lists many currently available tools.

TABLE 10-3 UPS POWER MANAGEMENT TOOLS

| Utility | File | Description |
| :--- | :--- | :--- |
| Apcd | apcd-0.5.tar.gz | Monitor APC SmartUPS in "smart" mode |
| Apcupsd | apcupsd-3.3.0.bin.linux.tar.gz | UPS power management in "dumb" mode for APCC Products |
| DumpUPSd | dumbupsd-0.1.tar.gz | Provides scripts for startup and shutdown for dump UPS |
| Genpower | genpower-1.0.1.tgz | Highly configurable UPS monitor |
| Powerd | powerd-2.0.tar.gz | Network-aware daemon that powers up and powers down hosts connected to dumb UPSs |
| SmartUPS | smartups-1.1.tgz | X11 Load monitor for SmartUPS |
| Upsd | ups.tar.gz | Program to interact with Powerbox UPS |
| Upsd Power Monitor Daemon | upsd-1.0.tgz | Monitor APC BackUPS or SmartUPS in "dumb" mode |
| Usyd | usyd-2.0.0.tgz | Uninterrupted power supply monitor |

# Laptop Battery Status

Power-management support can be compiled directly into the Linux kernel. This means, for example, that you can shut down a laptop without having to turn it off manually. (In addition to kernel support, you can get utilities from <http://sunsite.unc.edu/pub/Linux/system/power>.) Table 10-4 lists laptop power management tools.