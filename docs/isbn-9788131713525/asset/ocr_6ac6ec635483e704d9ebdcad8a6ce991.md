hardware registers in the processor.³ Typically, a small amount of memory is made available at boot time to accommodate loading and decompressing the kernel and a ramdisk image. Trying to access code or data beyond these early limits will fail. Each architecture and platform might have different early limits for accessing memory. Values on the order of 8 to 16MB are not untypical. We must remember that any code we execute from machine_init, including our platform initialization, takes place in this context. If you encounter data access errors (PowerPC DSI exception⁴) while debugging your new kernel port, you should immediately suspect that you have not properly mapped the memory region your code is trying to access.

# 16.3 Platform Initialization

Following is a quick review of the code flow during early initialization. Figure 16-3 shows the flow of execution from the bootloader or bootstrap loader to your platform-initialization code.

From bootloader

![](bbox=[0.08, 0.5, 0.78, 0.64])

FIGURE 16-3
Platform initialization flow of control

The files head.S and setup.c are both found in the .../arch/ppc/kernel directory for the PowerPC architecture. Our custom platform-initialization file will be placed in the .../arch/ppc/platforms directory. In Figure 16-3, it is represented by the file myplat.c. We are now in a position to examine the platform-specific initialization file in detail.

³ The AMCC PPC405 is a perfect example of this. The interested reader is encouraged to examine the BAT registers in this processor.

⁴ Refer to the Programming Environments Manual referenced at the end of this chapter for details of the PowerPC DSI exception.