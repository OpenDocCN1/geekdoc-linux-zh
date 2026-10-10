Code View:
`unsigned long pci_resource_{start|len|end|flags} (struct pci_dev *pdev, int bar);`

To operate on an I/O region such as the device control registers of a PCI video card, the driver needs to do the following:

+   1. Get the I/O base address from the appropriate base address register (bar) in the configuration space:
+      `unsigned long io_base = pci_resource_start(pdev, bar);`
+      This assumes that the device control registers for this card are mapped to the memory region associated with `bar`, whose value can range from 0 through 5, as shown in Table 10.2.
+   
+   2. Mark this region as being spoken for, using the kernel's `request_region()` regulatory mechanism discussed in Chapter 5, "Character Drivers":
+      `request_region(io_base, length, "my_driver");`
+      Here, `length` is the size of the control register space and `my_driver` identifies the region's owner. Look for the entry containing `my_driver` in `/proc/ioports` to spot this memory region.
+   
+      You may instead use the wrapper function `pci_request_region()`, defined in `drivers/pci/pci.c`.
+   
+   3. Add the register's offset obtained from the data-sheet, to the base address gleaned in Step 1. Operate on this address using the `inb()` and `outb()` family of functions discussed in Chapter 5:
+      ```c
+      /* Read */
+      register_data = inl(io_base + REGISTER_OFFSET);
+      /* Use */
+      /* ... */
+      /* Write */
+      outl(register_data, iobase + REGISTER_OFFSET);
+      ```

To operate on a memory region such as the frame buffer on the above PCI video card, follow these steps: