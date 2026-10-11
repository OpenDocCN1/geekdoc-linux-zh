Most system administrators configure a new Linux server by first installing a base system from one of the widespread distributions, such as RedHat, SuSE, or TurboLinux. This installation fulfills two basic purposes. It conveniently installs a coherent, compatible set of compilers, kernel source files, file management utilities, and other utilities and subsystems. It also installs a bootable kernel on the server or workstation with which the administrator can then create the desired configuration.

Once the base system is installed, the diligent system administrator should then compile the kernel as needed. Most system administrators will want to change the processor support for their kernels. Many distributions still install a kernel for the most common denominator, the i486 type of CPU. By compiling his or her own kernel, the system administrator can tell the kernel configurator to prepare the kernel for a specific type of CPU, which nowadays—especially on servers—is often a Pentium II or Pentium III. Some administrators might want to have SCSI support in the kernel, or ISDN if needed.

The prospect of having to compile and install a new kernel seems a dangerous and daunting task to many. You might be afraid of doing something wrong, and making it impossible to boot the machine. It is true that there is a certain risk of doing things the wrong way, as there is with all system administrator tasks. This is why it is best to compile the new kernel immediately after installation. If something goes wrong, the system can be reinstalled from scratch, without wasting too much of your time. Making such a mistake later on, after you have installed additional software (such as a database manager), would prove much more painful. There is no need to worry, however. Compiling a kernel and installing it is simpler than many might think.

![](bbox=[0.15, 0.68, 0.21, 0.77])

**Careful! *Apply all necessary kernel source patches before compiling the kernel. The links to obtain generic kernel patches are at www.linuxhq.com.*

# ## Source Code Tree Structure

To patch a kernel and compile it, as well as to help you better understand the information in upcoming chapters, it is helpful to have a good overview of the source code tree structure.