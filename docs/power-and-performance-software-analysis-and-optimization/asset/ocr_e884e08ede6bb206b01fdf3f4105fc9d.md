# CHAPTER 3 Intel® Core™ Processors

Atom™ processors are architected to meet the needs of smaller form factors, such as phones, tablets, netbooks, and microservers. The Intel® Quark™ microcontrollers are architected to meet the needs of the Internet of Things.

Additionally, Intel adopted a Tick T model for processor design. Each task, which is followed by a tick, introduces a new microarchitecture. Each tick, which is followed by a tick, improves the manufacturing process technology for the processor’s power consumption and thermal output. For the example, the Second Generation Intel® Core™ processor family was a tick, manufactured with 32nm manufacturing process technology. The Third Generation Intel® Core™ processor family was a tick, manufacturing the Second Generation microarchitecture with 22nm manufacturing process technology. The Fourth Generation Intel® Core™ processor family is a tick, introducing a new microarchitecture manufactured with the 22nm manufacturing process technology.

This focuses on the power management functionality added to the Intel® Architecture.

# 3.1 INTEL® PENTIUM® M

The Intel® Pentium® M processor family was introduced in 2003. This family consists of mobile processors, the “M,” and exemplifies many of the fundamental power management techniques available for Intel Architecture.

# 3.1.1 ACPI

The first revision of the Advanced Configuration and Power Interface (ACPI) specification was released in 1996. While ACPI is most commonly associated with power management, the majority of the ACPI specification actually deals with device enumeration and configuration. At boot, UEFI or the legacy BIOS is responsible for creating a series of tables that describe the devices available in the system and supported configurations.

Additionally, these ACPI tables, expose functions, written in the ACPI Machine Language (AML). The Linux kernel interpreter can parse and execute these functions. This allows for device code to be abstracted behind a standardized device interface, and for the kernel to control certain devices without requiring a specialized driver.

ACPI also defines a series of processor, device, and system states. The most-visible of these states are the S and G states, which include that most laptop users know as sleep and hibernation. There are three important ACPI processor states to understand.

The first thermal states, which are often referred to as T states, are responsible for automatically throttling the processor in the case of a thermal trip. In other words, these states are built into the processor to automatically prevent damage caused by overheating. Since a misconfiguration of the T states could result in physical damage,