This chapter addresses topics related to booting and shutting down the system. The first section covers key aspects of the system firmware on Sun SPARC platforms, including the *Boot PROM* test objectives. The second section summarizes the boot process for SPARC and Intel x86 platforms and covers the *Boot Process* test objectives. The third section describes system run levels, the services available at the different run levels, and how to change between run levels. It also describes how to add custom services at a selected run level and includes the *Initialization and Shutdown* test objectives.

# Boot PROM Firmware (OpenBoot)

A system’s boot Programmable Read-Only Memory (PROM) stores the firmware that is executed immediately after the system hardware finishes the Power On Self Test (POST). This firmware, called OpenBoot, is the standard firmware for Sun systems. OpenBoot firmware pertains only to SPARC platforms, but some limited compatible functionality is available on Intel x86 platforms as well.

OpenBoot is used to boot the operating system, run diagnostics, modify boot-related parameters stored in nonvolatile RAM (NVRAM), and provide a Forth interpreter used to execute the Forth Monitor.

Currently, two supported versions of OpenBoot are available: version 2.x and version 3.x. OpenBoot 2.x was introduced with SPARCstation 2 and SPARCstation IPX systems. OpenBoot 3.x is an enhanced version of OpenBoot 2.x; it’s based on the Institute of Electrical and Electronics Engineers (IEEE) Standard 1275-1994, “Standard for Boot Firmware.” OpenBoot 3.x is used on Sun Ultra series and newer SPARC platforms.

OpenBoot provides a command-line interface for the system console. The command-line interface has two modes:

+   - **Restricted Monitor**—Allows the administrator to boot the operating system, continue a suspended operation, or start the Forth Monitor. The prompt for the Restricted Monitor is the `>` symbol.
+   - **Forth Monitor**—Allows the administrator to boot the operating system, run diagnostics, and modify system configuration parameters. The prompt for the Forth Monitor is the word *ok*, which is typically referred to as the *OpenBoot prompt*.

System configuration parameters are stored in the system NVRAM. These parameters determine the system’s initial configuration and related communication characteristics and retain their value even if the power to the system is shut off.