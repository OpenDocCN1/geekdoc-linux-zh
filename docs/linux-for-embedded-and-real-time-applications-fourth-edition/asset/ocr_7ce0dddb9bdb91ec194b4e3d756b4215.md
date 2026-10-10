connect to the Internet of Things will likely be too small to run Linux. Nevertheless, these devices can benefit from running an operating system. Whereas Linux is a full-blown operating system with a kernel, device driver model, file systems, network stack, and a large collection of utilities, many alternatives are really just the kernel that handles scheduling, synchronization, and interrupts, and perhaps manages memory.

There are a great many operating systems out there, both open source and proprietary, but two stand out in my mind as being worth discussing.

# FreeRTOS

FreeRTOS is an open source project designed to be small and simple. It was originally written by Richard Barry, who subsequently formed Real Time Engineers Ltd. to provide commercial support. It has been ported to 35 microcontrollers. FreeRTOS is distributed under the GPL version 2 with an exception and a restriction. The exception allows you to retain your application code as proprietary, even when it is linked to the FreeRTOS kernel. The restriction is that “FreeRTOS may not be used for any competitive or comparative purpose, including the publication of any form of run time or compile time metric, without the express permission of Real Time Engineers Ltd.” The claim is that “this is the norm within the industry and is intended to ensure information accuracy.”

FreeRTOS is also available under a commercial license, called OpenRTOS, with additional features:

+   * A warranty. The open source version has no warranty.
+   * Professional technical support. The open source version is supported by a volunteer online community.
+   * IP infringement protection. Real Time Engineers Ltd. will defend commercial license holders against charges of patent or copyright infringement.
+   * No requirement to open source your changes to the RTOS kernel.

Another commercial product, SafeRTOS, extends FreeRTOS into the realm of safety critical systems, having been certified under a number of international safety standards. SafeRTOS is qualified for use in medical devices. Both OpenRTOS and SafeRTOS were developed by WITTENSTEIN High Integrity Systems in collaboration with Real Time Engineers Ltd.

FreeRTOS itself is just the kernel. On top of that is a whole ecosystem of packages called FreeRTOS + . These packages, some of which are open source while others are proprietary, support features such as:

+   * FAT file system
+   * UDP/IP