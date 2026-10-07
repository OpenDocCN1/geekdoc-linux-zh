them, and depend on the results. Evaluate the system load, configuration, and appropriateness of the hardware/software combination for the task. Ensure that the systems are as equal as you can make them, and then use the benchmarks for guidance.

# ## Selecting Hardware

There are many factors that determine how well a computer system will perform. Certainly the hardware plays a large part. Older or less capable hardware generally slows down a system. Anyone who has upgraded from a low-end processor to a top-rated processor can tell you the significance of the upgrade. Everything seems to go faster, even though only some functions have actually sped up. Now try running poorly configured software on a state-of-the-art machine. It runs better than on lesser hardware, but it is not the best that it can be. Reconfiguring will make a great difference provided that the hardware can handle the system load. Optimized software on low-end hardware is similarly disappointing. The trick is to optimize the software on the best hardware for the intended task.

Just as a car's engine can determine how fast it will go, the hardware components in your Linux system determine how it will perform. We'll look at the minimum acceptable hardware for a Linux system and some example architectures for different types of Linux systems. We'll also discuss some issues to consider in achieving optimal performance.

# ### Minimal Acceptable Hardware

One of the best-known facts about Linux is that it can make use of old computer parts that you have stored away somewhere. Many a high school student has salvaged an old 80386 machine and turned it into a decent print server or mail server. Originally, Linux was designed to install on an 80386 with as little as 4MB of memory, but with the rapid changes in processor speed and memory size, designing anything to work with only 4MB of memory became unnecessary. Red Hat requires at least 32MB of memory (recommends a minimum of 64MB) and 350MB (recommends a minimum of 650MB) of hard drive space (without X) for its 7.3 release. Other distributions have slightly different recommended requirements, but these don't reflect differences in the needs of identically configured systems; rather, they reflect differing default installations and usage assumptions.

Below is some basic information about selecting performance-oriented hardware for a Linux system.

# ### CPU Performance

One of the most important elements in determining a computer's performance is the Central Processing Unit (CPU). A new CPU seems to hit the market almost weekly. In the Intel-compatible x86 market, there are basically four players: Intel, Advanced Micro Devices, Inc. (AMD), VIA (which bought Cyrix in 1999), and startup Transmeta. New faces are appearing in the microprocessor technology market, but many target architectures other than the x86. Linux is known to run on all of those listed here:

+   - Intel/AMD/Cyrix 386SX/DX/SL/DLC/SLC
- Intel/AMD/Cyrix 486SX/DX/SL/SX2/DX2/DX4
- IDT WinChip
- NexGen NX586
- Cyrix 6x86, 6x86MX, and M-II

25