# BIOS

Basic input/output system. On PCs, EEPROM-based (page 1466) software that provides the lowest-level interface to peripheral devices and controls the first stage of the *bootstrap* (page 1457) process, which loads the operating system. The BIOS can be stored in different types of memory. The memory must be nonvolatile so that it remembers the systems settings even when the system is turned off. Also BIOS ROM. Refer to footnote 10 on page 921 for instructions on how to open the BIOS screens for maintenance.

# bit

The smallest piece of information a computer can handle. A *bit* is a binary digit: either 1 or 0 (*on or off*).

# bit-mapped display

A graphical display device in which each pixel on the screen is controlled by an underlying representation of zeros and ones.

# blank character

Either a *SPACE* or a *TAB* character, also called *whitespace* (page 1501). Also, in some contexts, *NEWLINES* are considered blank characters.

# block

A section of a disk or tape (usually 1,024 bytes but shorter or longer on some systems) that is written at one time.

# block device

A disk or tape drive. A block device stores information in blocks of characters. A block device is represented by a block device (block special). Contrast to *character device* (page 1460).

# block number

Disk and tape *blocks* (page 1457) are numbered so that GNU/Linux can keep track of the data on the device.

# blocking factor

The number of logical blocks that make up a physical block on a tape or disk. When you write 1K logical blocks to a tape with a physical block size of 30K, the blocking factor is 30.

# boot

See *bootstrap*.

# boot loader

A very small program that takes its place in the *bootstrap* process that brings a computer from off or reset to a fully functional state. See *Boot Loader* on page 1039.

# bootstrap

Derived from “Pull oneself by one’s own bootstraps,” the incremental process of loading an operating system kernel into memory and starting it running without any assistance. Frequently shortened to *boot*.

# Bourne Again Shell

bash. GNU's command interpreter for UNIX, bash is a POSIX-compliant shell with full Bourne syntax and some C commands built in. The Bourne Again Shell supports emacs-style command line editing, job control, functions, and online help.