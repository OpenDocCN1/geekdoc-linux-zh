# Paralle Printer

You need this option to add a parallel-port printer, but keep in mind that this module supports the printer, not the port. You will also need to install and configure the parallel port (parport) module. Also, by default, the lp.o module will install itself on all available ports unless specified by bootparams.

# I²C Support

This option adds support for the alternate devices on Matrox graphics cards; this is a feature that lets you add multiple independent monitors to the same console.

# Mice

These options are for bus mice and PS/2-style mouse connectors, as found in some lap-top computers. Note that although some laptops do support PS/2-style mice (such as the ThinkPad 560), the internal pointer may still be a plain COM1-based serial mouse.

# Watchdog, NVRAM, and RTC Devices

The watchdog timer enables a character device (mknod c /dev/watchdog c 10 130) used to reboot a locked machine. This feature is most often used with a watchdog dae-mon that will write to this device within the time limit. Linux includes support for a soft-ware watchdog and also for watchdog boards, which are not only more reliable, but several of them can also monitor the temperature inside your machine and force a shut-down/reboot when this rises above the allowed range.

The /dev/nvram option enables a new character device (mknod c /dev/nvram 10 144) for read/write access to the 50-byte CMOS memory.

All computers have a real-time clock; Linux lets you use it. This option will support a new character device (mknod c /dev/rtc 10 135) to generate reliable signals from 2Hz to 8kHz. The clock can also be programmed as a 24-hour alarm to raise IRQ8 when the alarm goes off. The rtc module is controlled by synchronized ioct1 calls and is most often used for high-frequency data acquisition where you don’t want to burn up CPU cycles polling through the time-of-day calls. Example code for using the rtc module can be found in Documentation/rtc.txt.

# DoubleTalk Speech Synthesizer

No surprises here, however users of speech synthesizers may also be interested in the Blinux (distribution for the blind) and Emacepspeak. Linux stands alone as the one OS that grants blind users total access to all functions of their computers and full access to all services on the Internet.