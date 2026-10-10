# # Looking at the Sources

PCI core and bus access routines live in `drivers/pci/`. To obtain a list of helper routines offered by the PCI subsystem, search for `EXPORT_SYMBOL` inside this directory. For definitions and prototypes related to the PCI layer, look at `include/linux/pci*.h`.

You can spot several PCI device drivers in subdirectories under `drivers/net/`, `drivers/scsi/`, and `drivers/video/`. To locate all PCI drivers, recursively grep the `drivers/` tree for `pci_register_driver()`.

If you do not find a good starting point to develop a custom PCI network driver, begin with the skeletal PCI network driver `drivers/net/pci-skeleton.c`. For a brief tutorial on PCI programming, look at `Documentation/pci.txt`. For a description of the PCI DMA API, read `Documentation/DMA-mapping.txt`.

Table 10.4 summarizes the main data structures used in this chapter. Table 10.5 lists the main kernel programming interfaces that you used in this chapter along with the location of their definitions.

| Data Structure | Location | Description |
| :--- | :--- | :--- |
| **pci_dev** | `include/linux/pci.h` | Representation of a PCI device |
| **pci_driver** | `include/linux/pci.h` | Representation of a PCI driver |
| **pci_device_id** | `include/linux/mod_devicetable.h` | Identity of a PCI card |
| **dma_addr_t** | `include/asm-your-arch/types.h` | Bus address of a DMA buffer |
| **scatterlist** | `include/asm-your-arch/scatterlist.h` | Scatter-gather list of DMA buffers |
| **sk_buff** | `include/linux/skbuff.h` | Main networking data structure (see Chapter 15 for more explanations) |

| Kernel Interface | Location | Description |
| :--- | :--- | :--- |
| **pci_read_config_byte()** | `include/linux/pci.h` | Routines to operate on the PCI |
| **pci_read_config_word()** | `drivers/pci/access.c` | configuration space. |
| **pci_read_config_dword()** | | |
| **pci_write_config_byte()** | | |
| **pci_write_config_word()** | | |
| **pci_write_config_dword()** | | |
| **pci_resource_start()** | `include/linux/pci.h` | These routines operate on PCI |
| **pci_resource_len()** | | I/O and memory regions to |
| **pci_resource_end()** | | obtain the base address, length, |
| **pci_resource_flags()** | | end address, and control flags. |
| **pci_request_region()** | `drivers/pci/pci.c` | Reserves PCI I/O or memory regions. |