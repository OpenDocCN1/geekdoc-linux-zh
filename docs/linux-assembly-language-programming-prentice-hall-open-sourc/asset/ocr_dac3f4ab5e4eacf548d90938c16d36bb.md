![](bbox=[0.15, 0.01, 0.85, 0.15])

# 8.3.1 Two-Tiered x86 Page Tables

Each table in this structure has 1024 four-byte entries. The size of each table therefore is 4K. Note that each table is also a page.

A page table table lists the locations of 1024 page tables. Each page table lists the locations of 1024 pages. Each page contains 4096 bytes. The total memory referenced by a page table table is therefore $1024 \times 1024 \times 4096 = 2^{10} \times 2^{10} \times 2^{12} = 2^{32} = 4$ Gigabytes. This is the size of one virtual address space.

# 8.3.2 Address Parsing

All virtual addresses are 32-bit quantities. These 32 bits are broken up as follows:

**32 bits = 10 bits + 10 bits + 12 bits.**

These bits are allocated as shown in *Figure 8-7*. The two ten-bit numbers are indices into tables with $1024 = 2^{10}$ entries. A ten-bit number is a number from 0 to 1023. The 12-bit number is an index into a page. A page has $2^{12}$ bytes. A 12-bit number is a number from 0 to 4095. It picks out one byte from a page.

![](bbox=[0.18, 0.47, 0.82, 0.58])

# 8.3.3 Translation Example

Suppose we have a virtual address of 1A2B3C4DH. This 32-bit address is broken into its three parts:

```
1    A    2    B    3    C    4    D
0001 1010 0010 1011 0011 1100 0100 1101   Virtual Address
0001 1010 00                          10 1011 0011                 Index into Page Table Table
                                100 0100 1101                       Index into Page
```

Translation begins at the page table table. The first ten bits pick out an entry from this table. In our example, these bits are: $0001\ 1010\ 00 = 0110\ 1000 = 68H = 104$. Indices start at zero. The first item fetched is the 105th four-byte entry in the page table table. If all goes well, this entry contains an address. In *section 8.3.4* it is shown how to extract this address. The address is the address of a page table. The next ten bits, $10\ 1011\ 0011$, equal $2B3H$, or 691, which is the number of an entry in the page table. Again if all goes well, we may extract an address from this entry. This address is the RAM address of the page on which the information being sought is located. Suppose that this address happens to be $1234000H$. The last 12 bits of the virtual address, $1100\ 0100\ 1101 = 0C4DH$, are the offset within the page. The translated address is then 1234C4DH.

# 8.3.4 Page Table Entries

Suppose a memory address is encountered by the processor for the first time in a read command such as