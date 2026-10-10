
## Accessing PCI Regions

PCI devices contain three addressable regions: configuration space, I/O ports, and device memory. Let’s learn how to access these memory regions from a device driver.

### Configuration Space

The kernel offers a set of six functions that your driver can use to operate on PCI configuration space:

```c
pci_read_config_(byte|word|dword)(struct pci_dev *pdev,
    int offset, int *value);
and
pci_write_config_(byte|word|dword)(struct pci_dev *pdev,
    int offset, int value);
```

In the argument list, `struct pci_dev` is the PCI device structure, and `offset` is the byte position in the configuration space that you want to access. For read functions, `value` is a pointer to a supplied data buffer, and for write routines, it contains the data to be written.

Let’s consider some examples:

- To decipher the IRQ number assigned to a card function, use the following:

```c
unsigned char irq;
pci_read_config_byte(pdev, PCI_INTERRUPT_LINE, &irq);
```

As per the PCI specification, offset `60` inside the PCI configuration space holds the IRQ number assigned to the card. All configuration register offsets are expressively defined in `include/linux/pci_regs.h`, so use `PCI_INTERRUPT_LINE` rather than `60` to specify this offset. Similarly, to read the PCI status register (two bytes at offset six in the configuration space), do this:

```c
unsigned short status;
pci_read_config_word(pdev, PCI_STATUS, &status);
```

- Only the first 64 bytes of the configuration space are standardized. The device manufacturer defines desired semantics to the rest. The Xircom card used earlier, assigns four bytes at offset `64` for power management purposes. To disable power management, the Xircom CardBus driver, `drivers/net/tulip/xircmod_cb.c`, does this:

```c
#define PCI_POWERMGT 0x40
pci_write_config_dword(pdev, PCI_POWERMGT, 0x0000);
```

## I/O and Memory

PCI cards have up to six I/O or memory regions. I/O regions contain registers, and memory regions hold data. Video cards, for example, have I/O spaces that accommodate control registers and memory regions that map to frame buffers. Not all cards have addressable memory regions, however. The semantics of I/O and memory spaces are hardware-dependent and can be obtained from the device data sheet.

Like for configuration memory, the kernel offers a set of helpers to operate on I/O and memory regions of PCI devices:

```c
unsigned long pci_resource_{start|len|end|flags} (struct pci_dev *pdev, int bar);
```

To operate on an I/O region such as the device control registers of a PCI video card, the driver needs to do the following:

1. Get the I/O base address from the appropriate base address register (bar) in the configuration space:
   ```c
   unsigned long io_base = pci_resource_start(pdev, bar);
   ```
   This assumes that the device control registers for this card are mapped to the memory region associated with `bar`, whose value can range from 0 through 5, as shown in Table 10.2.

2. Mark this region as being spoken for, using the kernel's `request_region()` regulatory mechanism discussed in Chapter 5, "Character Drivers":
   ```c
   request_region(io_base, length, "my_driver");
   ```
   Here, `length` is the size of the control register space and `my_driver` identifies the region's owner. Look for the entry containing `my_driver` in `/proc/ioports` to spot this memory region.

   You may instead use the wrapper function `pci_request_region()`, defined in `drivers/pci/pci.c`.

3. Add the register's offset obtained from the data-sheet, to the base address gleaned in Step 1. Operate on this address using the `inb()` and `outb()` family of functions discussed in Chapter 5:
   ```c
   /* Read */
   register_data = inl(io_base + REGISTER_OFFSET);
   /* Use */
   /* ... */
   /* Write */
   outl(register_data, io_base + REGISTER_OFFSET);
   ```

To operate on a memory region such as the frame buffer on the above PCI video card, follow these steps:

1. Get the base address, length, and flags associated with the memory region:

   ```c
   unsigned long mmiobase = pci_resource_start(pdev, bar);
   unsigned long mmio_length = pci_resource_length(pdev, bar);
   unsigned long mmio_flags = pci_resource_flags(pdev, bar);
   ```

   This assumes that this memory is mapped to the base address register, bar.

2. Mark ownership of this region using the kernel's `request_mem_region()` regulatory mechanism:

   ```c
   request_mem_region(mmiobase, mmio_length, "my_driver");
   ```

   You may instead use the wrapper function `pci_request_region()`, mentioned previously.

3. Obtain CPU access to the device memory obtained in Step 1. Certain memory regions, such as the ones that hold registers, need to guard against side effects, so they are marked as not being prefetchable (or cacheable) by the CPU. Other regions, such as the one used in this example, can be cached. Depending on the access flag, use the appropriate function to obtain kernel virtual addresses corresponding to the mapped region:

   ```c
   void __iomem *buffer;
   if (flags & IORESOURCE_CACHEABLE) {
       buffer = ioremap(mmiobase, mmio_length);
   } else {
       buffer = ioremap_nocache(mmiobase, mmio_length);
   }
   ```

   To be safe, and to avoid performing the preceding checks, use the services of `pci_iomap()` defined in `lib/iomap.c` instead:

   ```c
   buffer = pci_iomap(pdev, bar, mmio_length);
   ```

## Direct Memory Access

*Direct Memory Access* (DMA) is the capability to transfer data from a peripheral to main memory without the CPU’s intervention. DMA boosts the performance of peripherals manifold, because it doesn't burn CPU cycles to move data. PCI networking cards and IDE disk drives are common examples of peripherals relying on DMA for data transfer.

DMA is initiated by a *DMA master*. The PC motherboard has a DMA controller on the South Bridge that can master the I/O bus and initiate DMA to or from a peripheral. This is usually the case for legacy ISA cards. However, buses such as PCI can master the bus and initiate DMA transfers. CardBus cards are similar to PCI and also support DMA mastering. *PCMCI*A devices, on the other hand, do not support DMA mastering; but the *PCMCI*A controller, which is usually wired to a PCI bus, might have DMA mastering capabilities.

The issue of *cache coherency* is synonymous with DMA. For optimum performance, processors cache recently accessed bytes, so data passing between the CPU and main memory streams through the processor cache. During DMA, however, data travels directly between the DMA controller and main memory and, hence, bypasses the processor cache. This evasion has the potential to introduce inconsistencies because the processor might work on stale data living in its cache. Some architectures automatically synchronize the cache with main memory using a technique called *bus snooping*. Many others rely on software to achieve coherency, however. We will learn how to perform coherent DMA operations after introducing a few more topics.

DMA can occur *synchronously* or *asynchronously*. An example of the former is DMA from a system frame buffer to an LCD controller. A user application writes pixel data to a DMA-mapped frame buffer via `/dev/fbX`, while the LCD controller uses DMA to collect this data synchronously at timed intervals. We discuss more about this in Chapter 12, "*Video Drivers*". An example of asynchronous DMA is the transmit and receive of data frames between the CPU and a network card discussed in Chapter 15, "*Network Interface Cards*".

System memory regions that are the source or destination of DMA transfers are called *DMA buffers*. If a bus interface has addressing limitations, that'll affect the memory range that can hold DMA buffers. So, DMA buffers suitable for a 24-bit bus such as ISA can live only in the bottom 16MB of system memory called *ZONE_DMA* (see the section "*Allocating Memory*" in Chapter 2, "*A Peek Inside the Kernel*"). PCI buses are 32-bits wide by default, so you won't usually face such limitations on 32-bit platforms. To inform the kernel about any special needs of DMA-able buffers, use the following:

```c
dma_set_mask(struct device *dev, u64 mask);
```

If this function returns success, you may DMA to any address that is *mask* bits in length. For example, the e1000 PCI-X Gigabit Ethernet driver (`drivers/net/e1000/e1000_main.c`) does the following:

```c
if (!(err = pci_set_dma_mask(pdev, DMA_64BIT_MASK))) {
    /* System supports 64-bit DMA */
    pci_using_dac = 1;
} else {
    /* See if 32-bit DMA is supported */
    if ((err = pci_set_dma_mask(pdev, DMA_32BIT_MASK))) {
        /* No, let's abort */
        E1000_ERR("No usable DMA configuration, aborting\n");
        return err;
    }
    /* 32-bit DMA */
    pci_using_dac = 0;
}
```
