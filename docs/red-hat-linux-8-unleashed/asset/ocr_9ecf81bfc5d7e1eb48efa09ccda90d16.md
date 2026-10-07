# CHAPTER 2 Preparing to Install Red Hat Linux

+   * Along the same lines, CPU and motherboard overheating will cause problems. Proper attachment of the CPU's heatsink using a quality thermal paste (never use thermal tape), along with one or more fans providing adequate airflow will lessen the chance of hardware damage and system failure.

+   * You can run into problems if you switch the CPU installed in your computer, and especially if your PC's BIOS does not automatically recognize or configure for newly installed mainboard hardware and components. In some instances, a system restart is warranted, but BIOS issues should be resolved.

+   * Not all CPUs support Symmetric Multi-Processing, or SMP. Red Hat Linux readily supports of two or more CPUs, and during installation will automatically install an appropriate Linux kernel. You can avoid problems by reading the Linux HOWTO (available through http://www.tldp.org). Note that some CPUs, such as the current prop of VIA Cs, may not be used for SMP. Also motherboards require all CPUs to be identical. This means you need two identical CPUs in order to take advantage of SMP.

+   * Faulty or bad memory will cause Linux kernel panics or Signal 11 errors (segmentation faults) causing a system crash or a program to abort execution. Linux is quite sensitive to faulty hardware, but will run with great stability in a correctly configured system with good hardware. Problems can arise from incorrect BIOS settings, especially if video memory must occupy or use a portion of RAM. Always install quality (and appropriate) memory in your PC to avoid problems.

# Preparing and Using a Hardware Inventory

Buying a turn-key Linux solution is one way to avoid hardware problems, and many vendors are standing by, ready to prescribe solutions. However, managing deployments aimed at using existing hardware requires information collection.

If you are small business or individual user, you are well-advised to prepare detailed checklists of existing hardware before migrating to Red Hat Linux. Not only will you benefit from the collected information, but you might also be able to sidestep or anticipate problems before, during, or after installation. Problems are most likely to occur with newer hardware, cutting-edge hardware such as new motherboard chipsets and cards, or extraneous hardware such as operating system-specific scanners, printers, or wire-devices.

Table 2.2 provides a comprehensive checklist you can use to take inventory of target hardware, such as the computer and all peripherals. Veteran Red Hat users can take the collected information to build custom systems by adding known hardware or substituting cheaper than equivalent hardware.