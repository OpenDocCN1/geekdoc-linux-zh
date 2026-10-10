try to push your CPU to higher speeds, but this approach is not recommended if your aim is system stability. The Linux kernel reports the recognized CPU speed on booting (which you can view by using the `dmeg` command).

+   Along the same lines, CPU and motherboard overheating will cause problems. Proper attachment of the CPU's heatsink using a quality thermal paste (never use thermal tape), along with one or more fans providing adequate airflow lessens the chance of hardware damage and system failure.

+   You can run into problems if you switch the type of CPU installed in your computer, and especially if your PC's BIOS does not automatically recognize or configure for newly installed motherboard hardware and components. In some instances, a system reinstall is warranted, but BIOS issues should be resolved first.

+   Not all CPUs support symmetric multiprocessing, or SMP. Fedora readily supports use of two or more CPUs and, during installation, automatically installs an appropriate Linux kernel. You can avoid problems by reading the Linux SMP HOWTO (available through http://www.tldp.org/). Note that some CPUs, such as the current crop of VIA C3s, might not be used for SMP. Also, SMP motherboards require that all CPUs be identical. This means that you need two identical CPUs to take advantage of SMP.

+   Faulty or bad memory causes Linux kernel panics or Signal 11 errors (segmentation faults), causing a system crash or a program to abort execution. Linux is quite sensitive to faulty hardware, but runs with great stability in a correctly configured system with good hardware. Problems can arise from incorrect BIOS settings, especially if video memory must occupy and use a portion of system RAM. Always install quality (and appropriate) memory in your PC to avoid problems.

# ### Preparing and Using a Hardware Inventory

Buying a turn-key Linux solution is one way to avoid hardware problems, and many vendors are standing by, ready to prescribe solutions. However, managing deployments aimed at using existing hardware requires some information collection.

If you are a small business or individual user, you are well advised to prepare detailed checklists of existing hardware before attempting a migration to Linux. Not only do you benefit from the collected information, but you might also be able to sidestep or anticipate problems before, during, or after installation. Problems are most likely to occur with newer hardware, cutting-edge hardware such as new motherboard chipssets and video cards, or extraneous hardware such as operating system-specific scanners, printers, or wireless devices.

Table B.2 provides a comprehensive checklist you can use to take inventory of target hardware, such as the computer and any peripherals. Veteran Linux users can take the collected information to build custom systems by adding known hardware or substituting cheaper but equivalent hardware.