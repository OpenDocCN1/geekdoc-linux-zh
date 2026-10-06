# UNIX SYSTEM MANAGEMENT PRIMER PLUS

# How to Tell Whether a Power Supply Has Failed

It is easy to tell when a power supply fails on a system with only one power supply—the system shuts down. However, on systems with redundant power supplies, the symptoms are not as drastic. Most power supplies are equipped with LEDs that indicate whether they are functioning correctly. Other power supplies are integrated into the system itself, enabling the operating system to query the power supply's status. Check your system's documentation to determine the best method for detecting a failure.

Redundant power supplies also ease the process of migrating a machine to a different power source, eliminating downtime due to power interruptions during the move. If a server with a single power supply is plugged into a power strip on one of a rack, you'd have to power down the server to move the power cable to another strip. If the server had redundant power supplies, you could migrate one power cable at a time to the new strip, and the server would never be without power during the move.

True redundancy requires more than just redundant power supplies, To make redundant power supplies truly useful, the supplies cannot be connected to the same circuit. Otherwise, if one circuit goes down, all of the machine's redundant power supplies go down, so your production equipment should be plugged into two or more circuits if possible. If one circuit goes down, only one power supply will be without power, and your hardware will keep ticking.

Another way to ensure a minimum of downtime due to power failures is to use hot swappable power supplies. Hot swappable power supplies can be removed and replaced while the system is still running on a redundant power supply. If a power supply fails, there is never any downtime involved with its maintenance.

Not all hardware supports hot swappable power supplies, though; if not, a redundant power supply will keep the system running during a power failure, but the system will have to be taken down in order to replace the power supply.

# Using and Managing Power Cables

Of all the cables you work with as a system administrator, none will present you with as much variety as power cables. There are some, thin, some have round plugs, some have square ones, and plugs can have two, three, or four prongs. This wide variety of sizes and configurations ensures that the cables are sized adequately for the voltage they must carry, are grounded properly, and are compatible only with the appropriate power source. This last issue is important; unlike Ethernet or serial cables, power cables carry some serious electrical voltage, which if used improperly could cause injury, fires, or irreparable damage to your hardware. Special plug and outlet configurations prevent you from plugging the cable into the wrong power supply.

Both power receptacles (outlets) and their corresponding plugs are identified by NEMA (National Electrical Manufacturers Association) codes. For example, a plug rated for 125 volts (V) at 20 amperes (A or amp) has a different NEMA code and a different physical design than a