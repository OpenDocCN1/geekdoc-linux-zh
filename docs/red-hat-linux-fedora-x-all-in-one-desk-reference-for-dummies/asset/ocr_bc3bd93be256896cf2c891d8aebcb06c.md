# Rebuilding the Kernel 509

include configuration of multiport serial interface cards that enable you to connect multiple terminals or other devices to your Fedora Core system.

Other subcategories of character devices include

+   - Mice: You can include support for bus mice in this option category.
- Watchdog cards: You can enable support for special watchdog cards that can monitor the PC's status (including the temperature, for instance) and reboots the PC when necessary. This option can be helpful if you want to have a networked PC automatically reboot after it hangs up for whatever reason.
- Ftape or the floppy-tape device driver: If you have a tape drive connected to your floppy controller, you can configure it through this category of options.
- PCMIA card devices: These options are for configuring PC serial adapters that are meant for laptop PCs.

I2C Support
I2C — pronounced eye-squared-see is a protocol Philips has designed for communication over a pair of wires at rates between 10 and 100kHz. System Management Bus (SMBus) is a subset of the I2C protocol. Many modern motherboards have an SMBus mean for connecting devices such as EEPROM (electrically erasable programmable read-only memory) and chips for hardware monitoring. Linux supports the I2C and SMBus protocols. You need this support for video in Linux. If you have hardware sensors or video equipment that needs I2C support, set the I2C option to a dot (module) and show a dot for the specific device for your hardware. To find out more about the i2c, read the documentation in the /usr/src/linux*/Documentation/i2c-directory. In particular, the summary file describes the I2C and SMBus protocols.

Multimedia devices
This category of options configures support for multimedia devices such as video cameras, television tuners, and FM radio cards. For more information on these devices, consult the documentation in the /usr/src/linux*/ directory.

Sound
Use this set of options to configure sound-card support. If you have a sound card installed, start by enabling the Sound Card Support option. After that, click Advanced Linux Sound Architecture (ALSA) and select the options to build modules for the sound devices. You can always build the sound-modules for all types of sound cards. That way, the modules needed for your system's sound card are available when needed.