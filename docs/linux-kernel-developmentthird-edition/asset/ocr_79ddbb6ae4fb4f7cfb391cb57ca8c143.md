10 milliseconds). Other common values for HZ are 250 and 1000, corresponding to periods of 4ms and 1ms, respectively. Table 11.1 is a complete listing of the supported architectures and their defined tick rates.

Table 11.1 Frequency of the Timer Interrupt
| Architecture | Frequency (in Hertz) |
| :----------- | :------------------- |
| Alpha        | 1024                 |
| Arm          | 100                  |
| avr32        | 100                  |
| Blackfin     | 100                  |
| Cris         | 100                  |
| h8300        | 100                  |
| ia64         | 1024                 |
| m32r         | 100                  |
| m68k         | 100                  |
| m68knommu    | 50, 100, or 1000     |
| Microblaze   | 100                  |
| Mips         | 100                  |
| mn10300      | 100                  |
| parisc       | 100                  |
| powerpc      | 100                  |
| Score        | 100                  |
| s390         | 100                  |
| Sh           | 100                  |
| sparc        | 100                  |
| Um           | 100                  |
| x86          | 100                  |

When writing kernel code, never assume that HZ has any given value. This is not a common mistake these days because so many architectures have varying tick rates. In the past, however, Alpha was the only architecture with a tick rate not equal to 100Hz, and it was common to see code incorrectly hard-code the value 100 when the HZ value should have been used. Examples of using HZ in kernel code are shown later.

The frequency of the timer interrupt is important. As you already saw, the timer interrupt performs a lot of work. Indeed, the kernel's entire notion of time derives from the