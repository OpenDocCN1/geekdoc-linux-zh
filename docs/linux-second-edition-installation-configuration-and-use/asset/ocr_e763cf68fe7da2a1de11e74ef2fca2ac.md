# 206 CONFIGURATION AND ADMINISTRATION

| Code maturity level options | Taking devices | Network File Systems |
|---|---|--|
| Processor type and features | Wan interfaces | Partition Types |
| Loadable module support | Amateur Radio support | Native Language Support |
| General setup | | General setup |
| Plug and Play support | | |
| Block devices | ISDN subsystem | y n Networking support Help
| Networking options | CD-ROM drivers | y n Help
| | Character devices | y n PCI access mode Help
| SCSI support | Any | y n PCI quirks Help
| SCSI low level drivers | Mice | y n Help
| Network device support | Video For Linux Help
| ARConnect devices | Joystick support | y n Backward-compatible
| Ethernet (10 or 100mbit) | Flape, the floppy | y n WCA support Help
| Applet devices | Filesystems | y n System IPC Help
| | | Main Menu Next Prev

Figure 6.2 Kernel configuration under X.

doubt, please read the very informative help texts available for each option. However. if you have little experience with Linux or any other Unix, this information will confuse you. Therefore, this section presents further basic information on this subject without, however, dealing in depth with every single option.

# Fundamentals

Basically, you have to decide between two types of kernel: monolithic kernels contain all required drivers directly in the kernel and do not support modules. Modularized kernels are capable of including additional modules on top of the integrated kernels during current operation. As a rule, a modularized kernel is the better option. For many components, you have the choice between three alternatives: YES / MODULE / NO. YES means that this component is directly integrated into the kernel. MODULE means that this component is compiled as a modularized kernel), NO means that the component is not compiled at all. With sensible with a monolithic kernel, you must specify NO for all components that you do not require (otherwise the kernel becomes unnecessarily large). With a modularized kernel NO will save you some time (because the module does not have to be compiled), but you lose flexibility. Who knows whether you will not need this module at some point in the future?