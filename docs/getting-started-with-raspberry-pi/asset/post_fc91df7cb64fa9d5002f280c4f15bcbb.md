
# Index

## char
- device emulation
- drivers
- accessing char device emulation
- CMOS driver
  - I/O control
  - initialization
  - internal file pointer, setting with cmos_llseek()
  - opening
  - overview
  - reading/writing data
  - register layout
  - releasing
- code flow
- common problems
- data structures
- misc drivers
  - overview
  - parallel port communication
  - parallel port LED board
    - controlling with sysfs
    - led_c driver
- psuedo char drivers
- RTC subsystem
  - sensing data availability
    - fasync() function
    - overview
    - select()/poll() mechanism
- sources
- UART drivers
- watchdog timer
  - check_bugs() function
  - checklist for new devices
  - checksums
  - chip drivers [See NOR chip drivers.]
  - Chip Select (CS)
  - choosing
    - peripherals
    - processors
  - Circus Logic EP7211 controller
  - CIS (Card Information Structure)
    - cisparse_1 structure 2nd
    - cistpl.h file
    - cistpl_cftable_entry_t structure 2nd
  - class_create() function 2nd
  - class_destroy() function 2nd
  - class_device_add_attrs() function
  - class_device_create() function 2nd
  - class_device_create_file() function
  - class_device_destroy() function 2nd
  - class_device_register() function
  - class drivers
    - Bluetooth
    - HIDs (human interface devices)
    - mass storage
    - overview
    - USB-Serial
  - classes
    - device classes
    - input class
    - structure
  - clean markers
  - clear_bit() function
  - Clear To Send (CTS)

## clients
- client controllers
- EEPROM device example
- PCMCIA client drivers, registering

## clock
- clock_gettime() function
- CLOCK_INPUT_REGISTER
- clock_settime() function
- close() function

## CLUT (Color Look Up Table)
- CLut224

## CMOS
- CMOS_BANK0_DATA_PORT register
- CMOS_BANK0_INDEX_PORT register
- CMOS_BANK1_DATA_PORT register
- CMOS_BANK1_INDEX_PORT register
- cmos_dev structure
- CMOS drivers
  - I/O Control
  - initialization
  - internal file pointer, setting with cmos_lseek()
  - opening
  - reading/writing data
  - register layout
  - releasing
- cmos_fops structure
- cmos_init() function
- cmos_ioctl() function
- cmos_lseek() function
- cmos_open() function
- cmos_read() function
- cmos_release() function
- cmos_write() function

## code
- division multiple access (CDMA) 2nd
- portability
- codec_write_reg() function
- coding styles
- coldplug
- collect_data() function
- color modes

## command
- line utilities [See specific utilities.]
- set 0001
- set 0002
- set 0020
- COMMAND_REGISTER
- [See specific commands.]

## Common
- Flash Interface (CFI)
- memory (PCMCIA)
- UNIX Printing System (CUPS)
- Compact Flash [See CF (Compact Flash).]
- compact middleware

## compilation
- GCC compiler
- line disciplines

## complete
- complete() function 2nd
- complete_all() function
- complete_and_exit() function 2nd

## Complete
- Fair Queueing (CFQ) 2nd
- Completely Fair Scheduler (CFS)
- completion interface
- completion structure

## Complex
- Programmable Logic Devices (CPLDs) 2nd

## concurrency
- atomic operators

## CVS
- Concurrent Versioning System) 2nd

## debugging
- NICs (network interface cards)
  - overview
  - reader-writer locks
  - spinlocks and mutexes
- Concurrent Versioning System (CVS) 2nd
- CONFIG_4KSTACKS configuration option
- CONFIG_DEBUG_BUGVERBOSE configuration option
- CONFIG_DEBUG_HI_MEM configuration option
- CONFIG_DEBUG_PAGE_ALLOC configuration option
- CONFIG_DEBUG_SLAB configuration option
- CONFIG_DEBUG_SPINLOCK configuration option
- CONFIG_DEBUG_STACK_USAGE configuration option
- CONFIG_DEBUG_STACKOVERFLOW configuration option
- CONFIG_DETECT_SOFTLOCKUP configuration option
- CONFIG_IKCONFIG_PROC configuration option
- CONFIG_MAGIC_SYSRQ configuration option
- CONFIG_MyPROJECT_FASTBOOT marker
- CONFIG_MyPROJECT marker
- CONFIG_PCMCIA_DEBUG macro
- config_port() function
- CONFIG_PREEMPT_RT patch-set
- CONFIG_PREEMPT configuration option
- CONFIG_PRINTK_TIME configuration option
- CONFIG_RTC_CLASS configuration option
- CONFIG_SYSCTL configuration option
- configuration
  - kernel hacking configuration options
  - MTD
  - NAND
  - chip drivers
  - net_device structure
  - NICs
  - PCI resources
  - Wireless Extensions
- configuration space (PCI), accessing
- connectivity of embedded drivers
- conservative governor
- consistency of checksums
- consistent DMA access methods
- console drivers
  - boot logo
  - cell phones
  - consoles
- Consumer Electronics Linux Forum (CELF)
- container_of() function 2nd 3rd
- contexts, interrupt
- contrast and backlight
- CONTROL_REGISTER 2nd
- controller area network (CAN)
- controllers
  - CAN (controller area network)
  - CS8900 controller
  - CDRAM controllers
  - ECC-aware memory controller
  - EHCl controller
  - host controllers
  - NAND flash controllers
  - OTG (On-The-Go) controllers
  - USB device controllers
  - USB host controllers
- coord.c application
- copy_eb20_map() function
- copy_from_user() function 2nd
- copy_to_user() function

## copying
- system memory maps

## copyleft
- (GNU)

## correctable
- errors (CEs)

## counters
- preemption counters
- TSC (Time Stamp Counter)

## CPLDs
- Complex Programmable Logic Devices) 2nd

## cpgarray
- driver

## cpufreq
- cpufreq_register_governor() function
- CPU frequency (cpufreq) driver subsystem
- CPU frequency notification
- cpuspeed daemon

## crash
- command
- dumps

## create
- create_singlethread_workqueue() function
- create_workqueue() function

## CRT
- cathode ray tube

## crypto
- directory

## CS
- Chip Select)

## CS8900
- controller
- cs89x0_probe1() function

## cscope
- command

## CSR
- Cambridge Silicon Radio)

## ctags
- command

## CTS
- Clear To Send)

## CUPS
- Common UNIX Printing System)

## CVS
- Concurrent Versioning System) 2nd

## D-cache
- Data Cache)

## daemonize
- daemonize() function 2nd

## daemons
- acpid
- cardmgr
- cpuspeed
- iscsid
- oprofiled
- pppd
- trace

## DATA_REGISTER

## data
- availability, sensing
  - fasync() function
  - overview
  - select()/poll() mechanism
- Data Cache (D-cache)
- data field (sk_buff structure)
- data flow, Linux-PCMCIA subsystem
- data mixing (fn)
- data structures [See specific structures.]
- data transfer
  - DMA data transfer
  - net_device structure
  - NICs (network interface cards)
  - PCI
  - DMA descriptors and buffers
  - receiving and transmitting data
  - register layout of network functions
  - telemetry card example
  - USB

## DDWG
- Digital Display Working Group)

## deadline
- I/O scheduler 2nd

## dead
- state (threads)

## debugfs

## debuggers
- [See kernel debuggers.]

## debugging
- [See also ECC (error correcting code) reporting.]
- audio drivers
- block drivers
- Bluetooth
- breakpoints
- concurrency
- crash dumps
- diagnostic tools
- embedded Linux
- board rework
- debuggers
- I2C
- input drivers
- JTAG debuggers
- kdump
  - example
  - kexec with kdump
  - setup
  - sources
- kernel debuggers

## downloads

## entering
- gdb (GNU debugger)
- JTAG debuggers
- kdb (kernel debugger)
- Kdbg (kernel GNU debugger)
- overview

## kernel
- hacking configuration options
- kexec
  - invoking
  - preparation
  - sources
  - with kdump
- kprobes
  - example
  - fault-handlers
  - inserting inside kernel functions
  - jprobes
  - kretprobes
  - limitations
  - post-handlers
  - pre-handlers
  - sources
- Linux assembly
- LTP (Linux Test Project)
- MTD (Memory Technology Devices)
- overview 2nd 3rd
- PCI
- PCMCIA
- profiling
  - gprof
  - OProfile
  - overview
- RAS (reliability, availability, serviceability)
- test equipment
- tracing
- USB (universal serial bus)
- UML (User Mode Linux)
- watchpoints

## debug
- tool

## macros and functions
- DECLARE_COMPLETION() macro
- DECLARE_MUTEX() function
- DECLARE_WAITQUEUE() macro
- DEFINE_MUTEX() function
- DEFINE_TIMER() function
- DEFINE_TIMER() macro
- del_gendisk() function
- del_timer() function

## delay
- loop calibration
- delays
  - long delays
  - short delays

## delivery
- build scripts
- change markers
- checksum consistency
- code portability
- coding styles
- version control

## depmod
- utility

## descriptors
- USB)

## detect_memory_e820
- detect_memory_e820() function

## dev_alloc_skb
- dev_alloc_skb() function 2nd

## /dev
- directory
