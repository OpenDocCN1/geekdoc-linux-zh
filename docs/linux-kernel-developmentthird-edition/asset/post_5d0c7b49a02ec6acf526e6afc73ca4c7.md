
The internal storage in memory is different on big- versus little-endian, as shown in Table 19.3.

### Table 19.3 Big Versus Little Endian

| Address | Big Endian | Little Endian |
| :------ | :--------- | :------------ |
| 0       | 00000000   | 00000011      |
| 1       | 00000000   | 00000100      |
| 2       | 00000100   | 00000000      |
| 3       | 00000011   | 00000000      |

Notice how the big-endian architecture stores the most significant bytes in its smallest address. This is the exact inverse of little-endian.

As a final example, here is a simple code snippet to test whether a given architecture is big- or little-endian:

```c
int x = 1;

if (*(char *)&x == 1)
    /* little endian */
else
    /* big endian */
```

This works either in user-space or inside the kernel.

## History of Big- and Little-Endian

The terms *big-endian* and *little-endian* derive from Jonathan Swift’s 1726 satirical novel, *Gulliver’s Travels*. In the novel, the fictional Lilliputians’ major political issue is whether eggs should be cracked open on the big end or the little end. Those who favor the big end are big-endians, whereas those who favor the small are little-endians.

The similarity between the Lilliputians and our big-endian versus little-endian debate is that the argument is rooted deeper in politics than technical merits.

Each supported architecture in Linux defines one of `__BIG_ENDIAN__` or `__LITTLE_ENDIAN__` in `<asm/byteorder.h>` in correspondence to the machine’s byte order.

This header file also includes a family of macros from `include/linux/byteorder/`, which help with conversions to and from the various orderings. The most commonly needed macros are

```c
u32 __cpu_to_be32(u32);      /* convert cpu's byte order to big-endian */
u32 __cpu_to_le32(u32);      /* convert cpu's byte order to little-endian */
u32 __be32_to_cpu(u32);      /* convert big-endian to cpu's byte order */
u32 __le32_to_cpu(u32);      /* convert little-endian to cpu's byte order */
```

These convert from one byte order to another. In the case that the orders are the same (for example, if converting from native ordering to big-endian, and the processor is big-endian), the macros do nothing. Otherwise, they return the converted value.

## Time

The measurement of time is another kernel concept that can differ between architectures or even kernel revisions. Never assume the frequency of the timer interrupt or the number of jiffies per second. Instead, always use `HZ` to scale your units of time correctly. This is important because not only can the timer frequency differ among the various architectures, but it can also change on a given architecture from one kernel release to the next.

For example, `HZ` is 100 on the x86 platforms. That is, the timer interrupt occurs 100 times per second, or every 10 milliseconds. Earlier in the 2.6 kernel series, however, `HZ` was 1000 on x86. On other architectures, the value differs: Alpha has `HZ` equal to 1024 and `ARM` has it equal to 100.

Never simply compare `jiffies` to a number such as 100 and assume that always means the same thing. To scale time appropriately, multiply or divide by `HZ`. For example

```c
HZ          /* one second */
(2*HZ)      /* two seconds */
(HZ/2)      /* half a second */
(HZ/100)    /* 10 ms */
(2*HZ/100)  /* 20 ms */
```

`HZ` is defined in `<asm/param.h>`. The subject is discussed further in Chapter 10.

## Page Size

When working with pages of memory, never assume the page size. It is a common mistake for x86-32 programmers to assume that the page size is 4KB. Although this is true on x86-32 machines, other architectures have different sizes. Some architectures support multiple page sizes; in fact, Table 19.4 lists each support architecture’s valid page size(s).

### Table 19.4 Architecture Page Size(s)

| Architecture  | PAGE_SHIFT   | PAGE_SIZE          |
|:--------------|:-------------|:-------------------|
| alpha         | 13           | 8KB                |
| arm           | 12, 14, 15   | 4KB, 16KB, 32KB    |
| **avr**       | 12           | 4KB                |
| cris          | 13           | 8KB                |
| blackfin      | 12           | 4KB                |
| frv           | 14           | 16KB               |
| h8300         | 12           | 4KB                |
|               | 12, 13, 14, 16 | 4KB, 8KB, 16KB, 64KB |
| m32r          | 12           | 4KB                |
| m68k          | 12, 13       | 4KB, 8KB           |
| m68knommu     | 12           | 4KB                |
| mips          | 12           | 4KB                |
| mn10300       | 12           | 4KB                |
| parisc        | 12           | 4KB                |
| powerpc       | 12           | 4KB                |
| s390          | 12           | 4KB                |
| sh            | 12           | 4KB                |
| sparc         | 12, 13       | 4KB, 8KB           |
| um            | 12           | 4KB                |
| x86           | 12           | 4KB                |
| xtensa        | 12           | 4KB                |

When working with pages of memory, use `PAGE_SIZE` as the size of a page, in bytes. The value `PAGE_SHIFT` is the number of bits to left-shift an address to derive its page number. For example, on x86-32 with 4KB pages, `PAGE_SIZE` is 4096 and `PAGE_SHIFT` is 12. These values are defined in `<asm/page.h>`.

## Processor Ordering

Recall from Chapter 9, “An Introduction to Kernel Synchronization,” and Chapter 10 that architectures have varying degrees of processor ordering. Some have strict ordering constraints in which all loads and stores occur in the order prescribed by the code. Other chips have weak ordering, and loads and stores are reordered as the processor sees fit.

In your code, if you depend on data ordering, ensure that even the weakest ordered processor commits your load and stores in the right order by using the appropriate barriers, such as rmb() and wmb(). Chapter 10 has more information.

## SMP, Kernel Preemption, and High Memory

It might seem somewhat incorrect to include symmetrical multiprocesing, kernel pre-emption, and high memory in a discussion of portability. After all, these are not machine characteristics that affect an operating system, but instead they are features of the Linux kernel that are indeed somewhat architecture-agnostic. They represent, however, important configuration options that you should always assume are available in your code. That is, always program for an SMP/preempt/highmem system and you will always be safe, in any configuration. In addition to the previous portability rules, you need to follow these as well:

- Always assume your code will run on an SMP system and use appropriate locking.
- Always assume your code will run with kernel preemption enabled and use appropriate locking and kernel preemption statements.
- Always assume your code will run on a system with high memory (memory not permanently mapped) and use kmap() as needed.

## Conclusion

Writing portable, clean, proper code for the Linux kernel has two major implications:

- Always code for the greatest common factor: Assume anything can happen and any potential constraint is in place.
- Always assume that only the lowest common denominator is available: Do not assume any given kernel feature is available and require only the minimum architectural features.

Writing portable code requires awareness of many issues, including wordsize, data type size, alignment, padding, byte order, signedness, endianness, page size, and processor load/store ordering. In the majority of kernel programming, the primary concern is in ensuring that data types are used correctly. Nonetheless, one day an archaic architecture issue will arise, so it is important to understand portability issues and always write clean, portable code inside the kernel.

## Patches, Hacking, and the Community

One of the greatest benefits of Linux is the large community of users and developers that surround it. The community provides eyes to check your code, experts to provide advice, and users to test and report issues. Most important, the community is the final arbiter of what code is accepted into Linus' official kernel tree. Understanding how the system works is extremely important.

### The Community

If the Linux kernel community had to call somewhere home, it would be the *Linux Kernel Mailing List*. The Linux Kernel Mailing List (or as the regulars abbreviate it, just *lkm*) is the location of the majority of the announcements, discussions, debates, and flame wars over the kernel. New features are discussed, and most code is posted to the list before any action is taken. The list sees upward of 300 messages a day, so it is not for the faint of heart. Subscribing (or at least reading a digest or the archives) is recommended for anyone interested in serious kernel development. You can learn a lot simply by watching the wizards at work.

You can subscribe by sending the following message in plain text to majordomo@vger.kernel.org:

```
subscribe linux-kernel <your@email.address>
```

You can get more information at http://vger.kernel.org/ and a FAQ is available at http://www.tux.org/lkml/.

Numerous websites and other mailing lists pertain to the kernel specifically and Linux in general. An excellent resource for beginning kernel hackers is http://kernel-newbies.org/—a website that, of all things, caters to those cutting their teeth on the kernel. Two other excellent sources of kernel information are http://www.lwn.net/, Linux Weekly News, which has a great kernel news section, and http://www.kerneltrap.org/, Kernel Trap, which provides insightful commentary on kernel development.
