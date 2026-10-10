zeroed, and only the lower 42 bits are used. This allows us to concatenate the 22 bits of space register and 42 bits of offset to give a 64-bit GVA. We simply OR the 32-bit space register value with the upper 32 bits of the offset to get the 64-bit GVA. For example, if we have an address of `0x624b400.0x3fe'ff7c34e8`, the resulting GVA is `0x0624b7ff'ff7c34e8`.

This 64-bit GVA is used as the basis for address translation. In the next section we see how the 64-bit GVA is translated to a physical address.

# # Address Translation

Address translation is the process of translating a virtual address to a physical address. Before we begin the translation process, the virtual address is divided into a virtual page number (VPN) and an offset into that page. The VPN is then translated into a physical page number (PPN), and the offset is used as the offset into that physical page.

In PA-RISC 1.1, all pages are a fixed 4 KB long. This means that the offset portion of a virtual address is the lower 12 bits, and the VPN is the upper 20 bits. With PA-RISC 2.0, we introduced the concept of variable-sized pages. This means that the physical pages can be from 4 KB to 64 MB. However, for the purposes of address translation, we assume a 4-KB page size. Thus, we still use the upper 20 bits as the VPN. Once the VPN is translated to a PPN, we can determine how big the actual page is and thus how many bits of the address are used as the offset into the page. Figure 1-8 illustrates this translation process.

![](bbox=[0.2, 0.52, 0.75, 0.88])

Figure 1-8 Translation of Virtual Address to Physical Address