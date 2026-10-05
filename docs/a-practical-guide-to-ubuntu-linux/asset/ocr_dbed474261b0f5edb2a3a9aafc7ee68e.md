# 82 STEP-BY-STEP INSTALLATION

you want to add to the boot command line (discussed in the next section) and press RETURN to select the highlighted parameter. Press ESCAPE to close the list.

With the drop-down list closed, the ARROW keys can once again be used to move the highlight on the disk menu; the boot command line changes to reflect the highlighted selection.

On the Alternate and Server CDs, it offers Expert Mode. When you select this mode, the installer asks more questions about how you want to configure the system.

One special selection in this menu is Free software only. Selection installs free software only; it does not install proprietary software, including proprietary device drivers.

Alternatively, you can enter the parameters you wish to add after the double hyphen at the end of the displayed portion of the boot command line and press RETURN to boot your system. If you remove quiet and splash from this, Ubuntu displays information about what it is doing while it is booting (pages 57).

# BOOT COMMAND-LINE PARAMETERS (BOOT OPTIONS)

Following are some of the parameters you can add to the boot command line (see “Other Options” on the previous page). You can specify multiple parameters separated by spaces. See help.ubuntu.com/community/BootOptions (Common Boot Options) and the Linux BootPrompt-HowTo for more information.

+   - Disables ACPI (Advanced Configuration and Power Interface). Useful for systems that do not support ACPI or have problems with their ACPI implementation. Also acpi=off. The default is to enable ACPI.

+   - Disables APIC (Advanced Programmable Interrupt Controller). The default is to enable APM. Also apm=off.

+   - Disables DMRAID (Device-Mapper Software Raid), also called fake raid (page 41). The default is to enable DMRAID.

+   - Enables EDD (BIOS Enhanced Disk services).

+   - Turns off the framebuffer (video memory). Useful if problems occur when the graphical phase of the installation starts. Particularly useful for systems with LCD displays. Also framebuffer=false.

+   - Disables kernel handler interrupts. The default is to enable local APIC.

+   - Disables KMS (kernel-mode-setting technology), which may help some older graphics cards work properly. Include this parameter if the display does not work properly as you boot from a CD/DVD.