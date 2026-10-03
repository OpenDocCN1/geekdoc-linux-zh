NOTE
Solaris 8 introduced a new feature, which gives the ability to force a hanging system to halt. The new sequence to stop the system is Enter+~+Ctrl+B, which is equivalent to the Stop+A. There must be an interval of more than 0.5 seconds between characters, and the entire string must be entered in less than five seconds. This is true only with serial devices acting as consoles, and not for systems with keyboards of their own. If your console is connected to the serial port via a modem, you can send a break (Stop+A or L1+A) through the tip window by typing ~# (tilde+pound sign).

+   ♦ When the system is initially powered on. If your system is not configured to start up automatically, it will stop at the user interface. If automatic startup is configured, you can make the system stop at the user interface by pressing the Stop+A keys after the display console banner is displayed, but before the system begins starting the operating system.
♦ If the system hardware detects an error from which it cannot recover. (This is known as a Watchdog Reset.)

# OpenBoot Firmware Tasks

The primary tasks of the OpenBoot firmware are as follows:

+   ♦ Test and initialize the system hardware.
♦ Determine the hardware configuration.
♦ Start the operating system from either a mass storage device or a network.
♦ Provide interactive debugging facilities for testing hardware and software.
♦ Allow modification and management of system startup configuration, such as NVRAM parameters.

CAUTION
Forcing the system into the OpenBoot PROM using STOP+A or BREAK abruptly breaks execution of the operating system. It should be used only as a last effort to restart the system.

Specifically, OpenBoot will perform the following tasks necessary to initialize the operating system kernel:

+   1. Display system identification information and then run self-test diagnostics to verify the system’s hardware and memory. These checks are known as POST (Power-On Self-Test).
2. Load the primary startup program, bootblk, from the default startup device.
3. The bootblk program finds and executes the secondary startup program, ufsboot, and loads it into memory.

The ufsboot program loads the operating system kernel.