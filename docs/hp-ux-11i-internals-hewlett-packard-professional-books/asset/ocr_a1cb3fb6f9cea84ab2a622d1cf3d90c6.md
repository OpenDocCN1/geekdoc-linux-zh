be able to share memory with a 32-bit application. This is called mixed-mode access. In order to accommodate mixed-mode access, an area is set aside in quadrant 1 of the 64-bit layout. This area, starting at the 2 GB offset, corresponds with the beginning of quadrant 3 in 32-bit mode (also at the 2 GB offset).

![](bbox=[0.2, 0.2, 0.85, 0.58])

# **Explicit and Implicit Pointers, Narrow and Wide Mode**

When operating in narrow mode, we have to work with a 16-bit space ID and a 32-bit offset for a total of 48 bits. For performance reasons, it is desirable to have a method of specifying an address in a single 32-bit register. For this purpose, PA-RISC uses the concept of a *short pointer*. A short pointer uses the upper two bits of the register to specify a space register and the remaining 30 bits to specify an offset. Recall also that those upper two bits indicate the quadrant in which an address resides. Table 1-4 shows the relationship between the high-order bits of an address, the space register used to address it, and the quadrant.

As an example, the short pointer `0x40000782` refers to offset 0x782 in the space pointed to by space register 5. Another way of saying this is that `0x40000782` is in quadrant 2, which uses space register 5.

In wide mode, our short pointers are 64 bits long. We still use the first two bits to indicate the space register or quadrant, as described in Table 1-4. The following 20 bits in the short