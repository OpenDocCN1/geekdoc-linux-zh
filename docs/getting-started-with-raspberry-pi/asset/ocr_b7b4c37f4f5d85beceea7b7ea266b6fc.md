# ## Accessing PCI Regions

PCI devices contain three addressable regions: configuration space, I/O ports, and device memory. Let’s learn how to access these memory regions from a device driver.

# ### Configuration Space

The kernel offers a set of six functions that your driver can use to operate on PCI configuration space:

```
```
pci_read_config_(byte|word|dword)(struct pci_dev *pdev,
    int offset, int *value);
and
pci_write_config_(byte|word|dword)(struct pci_dev *pdev,
    int offset, int value);
```
```

In the argument list, `struct pci_dev` is the PCI device structure, and `offset` is the byte position in the configuration space that you want to access. For read functions, `value` is a pointer to a supplied data buffer, and for write routines, it contains the data to be written.

Let’s consider some examples:

+   - To decipher the IRQ number assigned to a card function, use the following:

```
```
unsigned char irq;
pci_read_config_byte(pdev, PCI_INTERRUPT_LINE, &irq);
```
```

As per the PCI specification, offset `60` inside the PCI configuration space holds the IRQ number assigned to the card. All configuration register offsets are expressively defined in `include/linux/pci_regs.h`, so use `PCI_INTERRUPT_LINE` rather than `60` to specify this offset. Similarly, to read the PCI status register (two bytes at offset six in the configuration space), do this:

```
```
unsigned short status;
pci_read_config_word(pdev, PCI_STATUS, &status);
```
```

+   - Only the first 64 bytes of the configuration space are standardized. The device manufacturer defines desired semantics to the rest. The Xircom card used earlier, assigns four bytes at offset `64` for power management purposes. To disable power management, the Xircom CardBus driver, `drivers/net/tulip/xircmod_cb.c`, does this:

```
```
#define PCI_POWERMGT 0x40
pci_write_config_dword(pdev, PCI_POWERMGT, 0x0000);
```
```

# ## I/O and Memory

PCI cards have up to six I/O or memory regions. I/O regions contain registers, and memory regions hold data. Video cards, for example, have I/O spaces that accommodate control registers and memory regions that map to frame buffers. Not all cards have addressable memory regions, however. The semantics of I/O and memory spaces are hardware-dependent and can be obtained from the device data sheet.

Like for configuration memory, the kernel offers a set of helpers to operate on I/O and memory regions of PCI devices: