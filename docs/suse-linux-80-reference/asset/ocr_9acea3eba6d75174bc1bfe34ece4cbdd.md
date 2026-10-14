**CLEAR_TEXTMF_FONTS="no"**
The automatical font generation for the TeX or LaTeX systems do locate the bitmap font into the directory `/var/cache/fonts/`. If CLEAR_TEXTMF_FONTS is set to yes, this directory will be cleared from fonts not used in the last 20 days.

**printer** – Drucker.

**DEFAULT_PRINTER="lp"**

Name of the printer queue used when lpr is invoked with no -P.

# Initializing Local Hardware (Keyboard, Modem, Mouse, PCMCIA)

**hardware** – Hardware Settings

**DEVICES_FORCE_IDE_DMA_ON=""**

Switch DMA on for the listed IDE devices.

**DEVICES_FORCE_IDE_DMA_OFF=""**

Switch DMA off for the listed IDE devices.

**clock** – time settings

**GMT="-u"**

If your hardware clock is set to GMT (*Greenwich Mean Time*), set this to -u. Otherwise set it to --localtime. This setting is important for the automatic change from and to daylight savings time.

**TIMEZONE="CET"**

The time zone is also important for the change from and to daylight savings time. This sets `/usr/lib/zoneinfo/localtime`.

**console** – Settings for the console: serial console, keyboard, framebuffer

**SER_CONSOLE_SESSION="console"**

Console session name

**SER_CONSOLE_SCREENRC="/usr/share/cyclades/screenrc"**

Screen configuration file

**SER_CONSOLE_OWNER="root"**

Owner of serial console session

**SER_CONSOLE_DEVICE="/dev/ttyC0"**

First serial console device, for example, `/dev/ttyC0` for Cyclades-Z.

**KEYTABLE="de-latin1-nodeadkeys"**

Defines the key layout. If you use a US keyboard, this variable can remain empty.