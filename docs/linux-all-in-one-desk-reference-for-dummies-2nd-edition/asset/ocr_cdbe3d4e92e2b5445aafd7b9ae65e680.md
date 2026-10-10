The Subarchitecture Type options enable you to select from different types of fundamental system designs that make use of the Intel x86 processor family but that may differ fundamentally from the well-known PC-compatible machines. Prior to version 2.6, the Linux kernel made an implicit assumption that the system’s architecture was based on the old IBM PC/AT family. Starting with kernel version 2.6, you can build the kernel for other types of Intel x86-based architectures, such as SGI visual workstation and multiprocessor systems with Non-Uniform Memory Access (NUMA). You probably can select the default PC-compatible Subarchitecture, but the other options are available if you have to build the kernel for a different type of x86-based system.

The next set of options prompt you for the processor family:

+   1. 386 (M386)
+   2. 486 (M486)
+   3. 586/ES/5x86/6x86/6x86MX (M586)
+   4. Pentium-Classics (M586TSC)
+   5. Pentium-MDX (M586MX)
+   6. Pentium-Pro (M686)
+   7. Pentium-II/Celeron (pre-Coppermine) (MPENTIUMII)
+   8. Pentium-III/Celeron (Coppermine) / Pentium-III Xeon (MPENTIUMIII)
+   9. Pentium M (MPENTIUMM)
+   10. Pentium-4/Celeron (P4-based) / Pentium-4 M/Xeon (MPENTIUM4)
+   11. K6 / K6-II / K6-III (MK6)
+   12. Athlon/Duron/K7 (MK7)
+   13. Opteron/Athlon64/Hammer/K8 (MK8)
+   14. Crusoe (MCRUSOE)
+   15. Efficeon (MEFFICEON)
+   16. Winchip-C6 (MWINCHIP6)
+   17. Winchip-2 (MWINCHIP2)
+   18. Winchip-2A/Winchip-3 (MWINCHIP3)
+   19. MediaGX/MXGede (MGEDEX)
+   20. CrixII/III/IVA-C3 (MCYRIXIII)
+   21. VIA C3-2 (Nehemiah) (MVIA C3_2)

If you select 386, the compiled kernel can run on any other processor (such as a 486 or any type of Pentium). However, if you’re creating a kernel specifically for your system’s processor, select your processor type from the list.

Subsequent options prompt you for a host of other processor-related options, which you can leave in their default settings. If in doubt, you can read the help for each option by pressing ? and select the ones that apply to your system.

# ## Power management options

This set of options deals with managing the system’s power and includes Advanced Configuration and Power Interface (ACPI), Advanced Power Management (APM) BIOS support, and CPU frequency scaling. You can simply accept the default settings for these options. If you don’t understand what an option means, press ? to get help on that option.