
## Opinion
### Coding column – Zach Samecha

![](img/c9d26cf718256f071c3af699b9670538_14_0.png)

Inevitably becomes a much larger problem, and a huge amount of code being produced, when combined with the important nature of its content, can result in major issues. A glitch in a video game is annoying for the gamer, but what if the faulty code is in a hospital machine or some financial software? Suddenly the consequences become much higher.

Any mistakes must be found and fixed, but it is essential that programmers are taught about them, why they matter and what the implications of these problems are. It is all very well that the skills drive wants to boost numbers, but quality control must also be brought into the mix.

It’s so exciting that growing numbers of people are getting stuck into coding, but we also have to make the industry look at what the impact on the quality of future code will be. Developers now have to code for the long term and make sure it won’t break after a few weeks, months or even years.

Thanks to the events of 2014, the world of programming has been brought into the spotlight like never before, which really is fantastic. Now in 2015, we need to take a step back to make sure that the code we are developing at present will stand the test of time in the future.

Above:
Coverity solutions help to build quality and security testing into the development process early

![](img/c9d26cf718256f071c3af699b9670538_14_1.png)

![](img/c9d26cf718256f071c3af699b9670538_15_0.png)

**Jon Masters** is a Linux kernel hacker who has been working on Linux for 19 years since he first attended university at the age of 13. Jon lives in Cambridge, Massachusetts, and works for a large enterprise Linux vendor. He publishes a daily Linux kernel mailing list summary at kernelopodcast.org

The most exciting new feature in Linux 4.0 is probably going to be the new live patching mechanism that can be used for dynamically updating the kernel with security and bug fixes without rebooting (akin to the older Ksplice and similar live updating technologies invented prior to that). Another cool feature will turn out to be the new KASan (Kernel Address Sanitizer), which tracks kernel memory accesses to verify that they turn out to be what it intends to touch. This should turn out to be very useful to developers, who generally like to know if any of their kernel modifications lead the kernel to attempt to trounce over physical RAM, causing hard-to-detect memory corruption in the process. Finally, the incorporation of support for NVM (Non-Volatile Memory) backed conventional filesystems will be exciting to those lucky enough to possess a large quantity of NVM hardware with which to try it out.

If things go according to plan, we’ll have a full summary of Linux 4.0 in next month’s issue, including how kernel live patching works. We will also look at how we root subtle bugs in the kernel during (and after) a development cycle by methodically investigating changes made over time, and a look back at how we dealt with the Linux 3.0 numbering change once of defe.

## Raspberry Pi 2

Many of us who grew up in the UK remember, rather fondly, the BBC Microcomputer System (or ‘BBC Micro’, or simply ‘BBC’). These computers were made by a small company from Cambridge, England, known as Acorn. The purpose of the original BBC was to bring computer literacy to the masses. Its cult-like success and the achievement of its goals during the early part of the Eighties was at least indirectly responsible for many later developments in the British computing industry, including the formation of another small company spin-off from Acorn now known as ARM. That’s the same ARM that today powers over 95 per cent of smartphones and the vast majority of tablets and other gadgets.

The original BBC inspired many who would come later. It was the inspiration for the creation of the Raspberry Pi Foundation years before the launch of their first Model A (a nod to the BBC, which like the Pi also came in a Model B) in 2012. The original Pi, which came in various models (A, A+, B and B+), leveraged a low-cost System-on-Chip originally designed for use as a mobile graphics processor and which just so happened to include a small ARMv6 (ARM1176JZF-S) compatible processor capable of running a full 32-bit Linux ARM stack (squeezed into the corner of the chip).

Former Broadcom ASIC Architect and Raspberry Pi Foundation trustee Eben Upton was among those who successfully convinced Broadcom to support the Pi project, developing a low-cost credit card sized computing platform that in three years has already sold over five million units. The original Pi featured a 700MHz single core ARMv6-compatible processor, 256MB (later 512MB) of RAM, an SDHC slot for storage and USB. The Pi used its on-chip USB to also provide wired Ethernet via a USB-to-Ethernet bridge chip, and was further expandable through HATs (Hardware Attached on Top) expansion boards.

While the original Pi was widely popular beyond even the most outlandish dreams of its

Linus Torvalds announced the closure of the Linux 4.0 merge window with the words, “let’s see how much, if anything, breaks due to the version number. Probably less than during the 3.0 timeframe, but I can just imagine somebody checking for meaningful versions.” This was yet another nod to the fact that Linux version numbers are, essentially, complete gibberish. They have no specific meaning, other than that which we assign for sentimental or emotional reasons, since each cycle follows the same pattern of development regardless.

![](img/c9d26cf718256f071c3af699b9670538_16_0.png)

### “While the original Pi was popular, it was not without its challenges”

supporters, it was not without its challenges. For one, the processor used by the original Pi – an ARMv6K compatible design – was intended really for use in embedded mobile designs. It used a version of the architecture that was ARM’s first cut at doing SMP (multiprocessing), even though it only provided a single core and was quickly superceded by the ARMv7 32-bit architecture that is otherwise in widespread use today. ARMv7 includes a standardised set of architectural features and ABIs that make generic Linux Operating System support for v7 based systems far easier than it is for older ARMv6 based designs like the original Pi.

For this reason, it was particularly exciting to learn of the launch of the second generation Raspberry Pi 2. The Pi 2 Model B features an identical board layout to the original Pi but it uses an updated Broadcom SoC, based on the contemporary quad-core ARM Cortex-A7, that is otherwise fully backward compatible with the original and matches the original’s $35 price point. This transition to a Cortex-A7 (the A7 has nothing to do with ARMv7, it’s just an ARM marketing term) brings with it the benefit of much broader operating system capability for the updated device. This is one reason why Microsoft is able to provide Windows 10 for the Pi 2. The Pi 2 is able to drive up runs most 32-bit ARM Linux distributions either out of the box or with relatively simple modifications. In Fedora, we call these “Remixes” as compared with the bigger upifts to rebuild the whole distros for v6 in the past.

As with the original, the initial Linux kernel port for the Pi 2 is available at github.com/raspberry/linux. The port is currently based upon kernel 3.18 and support for the Broadcom 2709 series SoC was merged on 2 February. That commit (github.com/raspberry/linux/commit/d9f6ac63a), dates from May 2013, so it has clearly been sitting on the shelf and ready to go for some time. Like most other contemporary ports to specific embedded platforms, Pi is more about wiring up existing drivers and architecture features than about incorporating huge amounts of new code. The port enables a few specifics common to any device building, using the BCM2709 SoC family, such as educating the kernel about it being based upon the ARMv7 architecture. The guts of the port are then provided by a file called arch/arm/boot/dts/bcm2709-rpi-2-b.dts.

The DeviceTree source (DTS) file for the Pi 2 describes the hardware of the Pi using a flexible hierarchical language that follows the documented reference bindings within the kernel’s documentation/devicetree directory. Each of the major devices and IP (Intellectual Property) blocks included within the design are matched against such a binding using the compatible property within this DTS. For example, the DTS informs the kernel that the Pi is compatible with the bcm2709, that it is named Raspberry Pi 2 Model B and that it includes certain hardware described with the SoC (chip) specific bcm2709.dts (DTS include file). This included file describes the SoC itself, including the 4 CPU cores, the interrupt controller used to service peripheral devices, the GPIO and other on-chip interfaces, and the generic armv7 timer.

The kernel port includes a bcm2709_defconfig file that the kernel can use to determine which configuration options should be used to build a minimal kernel binary tailored to boot on the Pi 2 (though it will use the compiled form of the DTS, known as a DTB – DeviceTree Blob – at runtime to actually determine which of the many possible drivers compiled into the kernel should be used). Finally, the port includes an old-style bcm2709_b. board-specific C file which seems to be more as a convenience for those not using a DeviceTree supporting bootloader (this provides further evidence that the port was originally made perhaps even longer ago than the 2013 date of this specific commit). The remaining code also provides some core enablement for all 270X Broadcom platforms.

Building and installing the kernel for the Pi 2 is relatively straightforward, with multiple options, ranging from a cross-compilation (on an x86 laptop) to local compilation on the device itself. This is documented at raspberry.pi.org. While the original Pi never really had a good upstream support story, it is the hope of this author that the second generation will be supported in a standard Linux kernel shipping in your favourite Linux distro soon enough.

Finally this month, Linux noted that the strongest argument for some people advocating a Linux 4.0 release seems to have been a wish to see 4.15 – because “that was the version of Linux skynet used for the T-800 terminator”! All the more reason to be afraid of the impending arrival of Linux 4.0 and our robotic overlords.
