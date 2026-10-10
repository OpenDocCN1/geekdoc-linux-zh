# What is a virus?

A virus is a program, which attaches itself to the original program code and runs whenever that authentic program runs with the intention of causing harm without the knowledge of the user. A computer virus normally reproduces itself without your knowledge or permission. Generally, they have an infection stage where they regenerate and the attack stage where they cause havoc.

Another definition of a virus will be a program, which re-duplicates or replicates its own code by attaching itself to another executable file in a way that the virus code is executed whenever the executable file is executed.

# Types of computer virus

A computer virus can be grouped into various ways, but in this book, I will classify them based on their orthogonal axes. This means we will look at viruses based on the type of target they try to infect along with the methods used to hide from been detected by anti-virus and users. One of the simple ways of categorizing viruses is based on what they try to infect. In this section, I will explore three of these ways, which include executable file infectors, boot-sector infectors, and macro viruses (data file infectors)

+   - **Boot Sector Infectors**
+   
+     In as much as the sequence of operation of the boot virus differs on different machines, it follows a simple process. You power on the system and the ROM-based instructions begin operation. It then performs self-test, device detection, and initialization test. Immediately the boot device is identified with the boot block read from the device, then control is sent to the loaded code. This entire process is known as the primary booting process. Furthermore, the code loaded during this process loads another larger program, which understands the file system structure of the boot device.