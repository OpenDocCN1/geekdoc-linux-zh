
- Organize all parts to be assembled. If more than one unit is to be built, collect like parts together *fin-style*.
- Provide sufficient flat space for assembly, including room for keyboard, mouse, and monitor used for initial check-out.
- Work in a well-lighted environment.
- Follow the same order of tasks in assembling all units; routine leads to reliability.
- Have a checklist, like this one, handy, even if it is used only as a reference.
- When first opening a case, collect screws and other small items in separate containers.
- Keep food and drink on another table to avoid the inevitable accident.

After you have done one or two systems, the process becomes much quicker. We find that we can assemble nodes in well under an hour once we become familiar with the idiosyncrasies of any particular configuration.

Many of the instructions below may not apply in every case. Included are directions for such subassemblies as monitors, keyboards, and sound cards that rarely show up in the majority of Beowulf nodes. Usually, however, at least one such node is more heavily equipped to support user interface, operations support, and external connections for the rest of the system.

In a number of cases, the specific action is highly dependent on the subsystems being included. Only the documentation for that unit can describe exactly what actions are to be performed. For example, every motherboard will have a different set and positioning of jumpers, although many of the modern boards are reducing or almost eliminating these. In these instances, all we can say is: “do the right thing,” but we still indicate in general terms the class of action to take place.

## 3.10.1 Motherboard Preassembly

- Set every jumper on the motherboard properly.
- Look through your motherboard manual and verify every setting, since the default may not work for your CPU, memory, or cache configuration.
- Locate every jumper and connector: floppy, hard drive, PS/2, COM port, LPT port, sound connectors, speaker connector, hard disk LED, power LED, reset switch, keyboard lock switch, and so forth.

- Install the CPU.
  - Processors are designed so that they can only be inserted correctly. Don’t force.
  - Whatever the chip, match the notched corner of the CPU with the notched corner of the socket.
  - When using a ZIF socket, lift the handle 90 degrees, insert the CPU, and then return the handle back to its locked position.

- Install the memory.
  - Main memory DIMM. Note pin 1 on the DIMM, and find the pin 1 mark on the motherboard. It is difficult to install 164-pin DIMMs incorrectly, but it is possible. Begin by placing the DIMM at a 45 degree angle to the socket of bank 0. The DIMM will be angled toward the rest of the DIMM sockets (and away from any DIMMs previously installed). Insert the DIMM firmly into the socket; then rotate the DIMM until it sits perpendicular to the motherboard and the two clips on each edge have snapped around the little circuit board. There may or may not be a “snap,” but you should verify that the two clips are holding the DIMM fast and that it doesn’t jiggle in the socket. Repeat this until you fill one, two, or more banks.
  - Cache memory (if so equipped). Some older units may have L2 caches on the motherboard, while newer processors include them within the processor module. Cache memory may be DIMM or SIMM; in any case, install it now.

## 3.10.2 The Case

- Open the case, remove all the internal drive bays, and locate all the connectors: speaker, hard disk LED, power LED, reset switch, keyboard lock switch, mother board power, peripheral power, and so forth.
- Mount the motherboard in the case.
  - ATX-style cases use only screws to mount the motherboard, and it is very straightforward.
  - AT-style power connector comes in two pieces and must be connected properly. The black wires *must be placed together* when they are plugged into the motherboard.
  - Ensure that the CPU cooling fan is connected to the power supply. This is usually a 4-pin male connector that goes to one of the power supply connectors.
- Plug in the keyboard, and see whether it fits.
- Plug in an adapter card, and see whether it fits.
- Start connecting the case cables to the motherboard.
  - Pull out floppy cables, hard disk cables, PS/2 mouse cable, and lights. Line up each pin 1 to the red side of cables.
- Install the speaker. It usually is a 4-pin connector with two wires (one red, one black, which can be installed either way on the motherboard).
- If your case has holes for COM ports and LPT ports, punch these out, and save a card slot by unscrewing the connectors that came on the slot-filler strip of metal, removing the connector, and mounting it directly on the case.
- Attach power cables to the motherboard.
  - ATX-style cases have only one power connector, which is keyed to only fit one way.

## 3.10.3 Minimal Peripherals

- **Floppy disk drive**
  - **Mechanical**
    - It may be necessary to reinstall the floppy mounting bay (if it was taken out previously).
    - The floppy drive must protrude from the front of the case. Take off one of the 3.5 inch plastic filler panels from the front of the case. Then slide the floppy drive in from the front until the front of the drive is flush with the front of the case. Using two small screws that are supplied with the case, attach the floppy drive’s left side. If the floppy drive bay is detachable, remove the bay with the floppy half installed, and with the drive bay out, install the screws for the right side.
    - If the drive bay is going to contain hard disks in addition to floppy drives, leave the drive bay out for now, and go to the hard disk installation section before putting the drive bay back into the case.
  - **Electrical**
    - The floppy disk needs two connections: one to the power supply, and one to the motherboard or floppy controller. The power supply connector is shaped to prevent you from getting it backwards.
    - Some floppy power connectors are smaller than the standard connector, and most power supplies come with one of these plugs. These connectors can be installed in only one way.
    - For data, a flat ribbon cable is needed. It is gray with 34 conductors and a red stripe to indicate pin 1. One end of the cable will usually have a twist in it. The twisted portion connects to a second floppy drive (drive B). The end farthest from the twist connects to the motherboard or floppy controller.
- **VGA card installation**
  - If the motherboard has an integrated video adapter, skip the next step.
  - Plug the VGA card into the appropriate slot, depending on the type of card purchased (PCI slot for a PCI card, ISA slot for an ISA card).
  - Screw the top of the metal bracket that is attached to the adapter into the case, using one of the screws supplied with the case.
- **Monitor**
  - Plug the monitor into a wall power outlet.
  - Plug the video input plug, which is a 15-pin connector, into the back of the video card.

## 3.10.4 Booting the System

Setup involves configuring the motherboard's components, peripherals, and controllers. The setup program is usually in ROM and can be run by pressing a certain key during POST. Check the CMOS settings using the setup program before booting for the first time. If you make changes, you will need to exit setup and save changes to CMOS for them to take effect. You will be able to change the date and time kept by the real time clock. Memory configuration such as shadow RAM and read/write wait states can be changed from their defaults. IDE hard disks can be detected and configured. Boot sequence and floppy drives can be configured and swapped. PCI cards and even ISA cards can be configured, and plug-n-play disabled (which should be done if running a non-Windows operating system). ISA bus speed can be changed and ports can be enabled or disabled.

IDE disks are almost always configured as auto detect or user-defined type. Use shadow video unless you have problems. Shadow the ROM of your network interface card (NIC) or SCSI card for better speed. For better speed and if you have EDO memory, you can usually use the most aggressive memory settings—just try it out before you stick with it to avoid corrupting data files.

Minimum requirements for booting the system are as follows:

- A bootable floppy disk
- Motherboard with CPU and memory installed
- Video card on the motherboard
- Floppy drive with one cable connected to it and power to it
- Monitor plugged into the wall and the video card
- Keyboard attached

To boot the system, proceed as follows:

- Making sure that the power switch is off, attach a power cord from the case to the wall.
- Turn on the monitor.
- Turn on the power to the PC, and get ready to shut it off if you see, hear, or smell any problems.
- Look for signs that all is working properly:
