
# Intel® Core™ Processors

## CHAPTER 3

## CHAPTER CONTENTS

- 3.1 Intel® Pentium® M...............................................................................44
  - 3.1.1 ACPI ........................................................................................ 44
  - P States and Intel SpeedStep® Technology ............................................ 45
  - C States .......................................................................................................... 46
- 3.2 Second Generation Intel® Core™ Processor Family ............................ 48
  - 3.2.1 Intel® HD Graphics ....................................................................... 49
  - 3.2.2 Intel® Flex Memory Technology ................................................ 49
  - 3.2.3 Intel® Turbo Boost Technology ................................................. 50
  - 3.2.4 Intel® RAPL ............................................................................... 51

References. the previous chapter, the Intel® Pentium® lineup of processors was introduced. At that time, mobility wasn't as pervasive as it is today. Of course, there were laptops and mobile users who cared about battery life and power consumption; however, for the majority of computer users, raw computational performance was their primary concern. This trend was reflected in the design of the Pentium Processors. While they did introduce new features for reducing power consumption, and there were mobile versions of some Pentiums, time was spent optimizing their performance.

Once again, the technological landscape was changing, with a new emphasis on reduced power consumption and smaller form factors. At the same time, these needs were compounded by a still increasing demand for raw computational performance. Whereas the Pentium needed to handle intense 3D games, the Intel® Core™ processor family needed to handle blistering 3D games that were played on battery power while waiting in the game store.

To accommodate these needs, Intel focused on architecting a series of new processors to improve performance while simultaneously reducing power consumption. The Intel® Xeon® processors are architected to meet the needs of data centers, workstations, HPC supercomputers, and enterprise infrastructure. The Intel® Core™ processors are architected to meet the needs of the consumer and business markets, including both desktop and mobile systems. These chips carry the logo of each Intel® Core™ i3, Intel® Core™ i5, or Intel® Core™ i7. The Intel® Atom™ processors are architected to meet the needs of smaller form factors, such as phones, tablets, netbooks, and microservers. The Intel® Quark™ microcontrollers are architected to meet the needs of the Internet of Things.

Additionally, Intel adopted a Tick T model for processor design. Each task, which is followed by a tick, introduces a new microarchitecture. Each tick, which is followed by a tick, improves the manufacturing process technology for the processor’s power consumption and thermal output. For the example, the Second Generation Intel® Core™ processor family was a tick, manufactured with 32nm manufacturing process technology. The Third Generation Intel® Core™ processor family was a tick, manufacturing the Second Generation microarchitecture with 22nm manufacturing process technology. The Fourth Generation Intel® Core™ processor family is a tick, introducing a new microarchitecture manufactured with the 22nm manufacturing process technology.

This focuses on the power management functionality added to the Intel® Architecture.

## 3.1 INTEL® PENTIUM® M

The Intel® Pentium® M processor family was introduced in 2003. This family consists of mobile processors, the “M,” and exemplifies many of the fundamental power management techniques available for Intel Architecture.

### 3.1.1 ACPI

The first revision of the Advanced Configuration and Power Interface (ACPI) specification was released in 1996. While ACPI is most commonly associated with power management, the majority of the ACPI specification actually deals with device enumeration and configuration. At boot, UEFI or the legacy BIOS is responsible for creating a series of tables that describe the devices available in the system and supported configurations.

Additionally, these ACPI tables, expose functions, written in the ACPI Machine Language (AML). The Linux kernel interpreter can parse and execute these functions. This allows for device code to be abstracted behind a standardized device interface, and for the kernel to control certain devices without requiring a specialized driver.

ACPI also defines a series of processor, device, and system states. The most-visible of these states are the S and G states, which include that most laptop users know as sleep and hibernation. There are three important ACPI processor states to understand.

The first thermal states, which are often referred to as T states, are responsible for automatically throttling the processor in the case of a thermal trip. In other words, these states are built into the processor to automatically prevent damage caused by overheating. Since a misconfiguration of the T states could result in physical damage, these states are completely independent of software. Obviously, tripping these states should be avoided by ensuring that the processor is cooled by a solution capable of handling its TDP. It is also important to be aware of the fact that thermal throttling will drastically reduce performance until temperatures have returned to safe levels. As a result, this is something to be cautious of when running long benchmarks or tests.

The rest of this section focuses on the other two processor states.

## P states and Intel SpeedStep® Technology

The ACPI specification defines the concept of Device and Processor performance states. Performance states, or simply P states, are designed to improve energy efficiency by allowing the processor to reduce performance, and therefore power consumption, when performance is not required. As of the latest ACPI specification, the performance states are defined as:

- **P0** While a device or processor is in this state, it uses its maximum performance capability and can consume maximum power (Unified EFI, Inc, 2014)
- **P1** In this performance state, the performance capability of a device or processor is limited below its maximum and consumes less than maximum power (Unified EFI, Inc, 2014)
- **Pn** In this state, the performance capability of a device or processor is at its minimum level and consumes minimal power while remaining in an active state. State ni is a maximum number and processor or device dependent. Resources and devices may define support for an arbitrary number of performance states not to exceed 16 (Unified EFI, Inc, 2014).

Notice that lower P states correspond to higher power consumption, while the higher P states correspond to lower power consumption. The specification uses P states provides each hardware with the flexibility of defining up to sixteen additional performance states. As a result, the number of supported P states for a given system varies depending on the exact processor configuration, and must be detected at runtime through the ACPI tables.

On Intel Architecture, these states are implemented via Enhanced Intel SpeedStep® Technology (EIST). EIST provides an interface for controlling the processor's operating frequency and voltage (Intel Corporation, 2004). This interface consists of various model registers for requesting a state transition, IA32_PERF_CTL_REGISTER, and for obtaining hardware feedback regarding the state, IA32_MPERF and IA32_APERF.

It is important to note that these states are requested, as opposed to being set by software. Many complex factors contribute to the actual P state processor is put into, as the requested by the other cores, the system's thermal state, and so on. Additionally, these MSRs are duplicated by Hyper-Thread, yet prior to the Fourth Generation Intel® Core™ processor family, P states were governed at the granularity of the processor package.
