# Virtual Memory System

In a virtual memory system, special memory management functions allow programs to address more memory than is physically installed in the system. This memory, known as virtual memory, appears to programs as a large amount of memory that can be mapped to physical memory. Data that is stored in virtual memory must be paged into physical memory for the CPU to use it, and then copied out to disk to make room in physical memory for another process. The process of paging in or paging out can be quite time-consuming and uses a lot of system resources. It bears repeating that access to disk is approximately 1,000 times slower than an access to memory. Paging should be avoided at all costs, even if it means reducing the size of the Oracle SGA.

# 32-bit vs. 64-bit Processors

The more powerful 64-bit processors have been available for well over a decade but have not become mainstream, because each 64-bit processor architecture was proprietary and was not supported by more than one operating system. Nonetheless, 64-bit processors offer several advantages over 32-bit processors, including the ability to address more memory and to process more information in a single clock cycle. Unfortunately, these 64-bit processors have not achieved the popularity of 32-bit processors. However, the new hybrid 64-bit / 32-bit processors are gaining popularity quickly. These processors are described in a few paragraphs.

# 32-bit Addressing

Various 32-bit architectures have been around for many years and are the most common architecture in production. Almost every PC uses a 32-bit processor from either Intel or AMD. The disadvantage of the 32-bit processor is that 32 bits can directly address a maximum of 4GB of RAM. In the past few years, there have been some workarounds by allowing more memory to be addressed via the Physical Address Extension (PAE).

PAE allows physical memory to be accessed above 4GB, but it does not increase the amount of virtual memory available to a process. Although it does allow for more

# Linux Paging and Swapping

Linux does not require as much swap space as most Unix operating systems. In fact it is not uncommon to find Linux systems with 4GB or more memory with 1GB or less swap space. Since swap space is used only when you run out of physical memory, theoretically the more memory that you have, the less chance that you will use the swap space.