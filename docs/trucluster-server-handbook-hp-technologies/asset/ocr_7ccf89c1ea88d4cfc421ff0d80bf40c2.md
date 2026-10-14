![](bbox=[0.087, 0.092, 0.901, 0.211])

![](bbox=[0.087, 0.229, 0.901, 0.351])

![](bbox=[0.087, 0.369, 0.901, 0.494])

![](bbox=[0.087, 0.511, 0.901, 0.627])

# A.1.5.2　Memory Channel Address Space Window Size

In order for redundant Memory Channel rails to function with 512MB address space window size, each Memory Channel must be located in separate PCI buses. You can use the “show config” command to determine the location of the Memory Channel cards.

```
```text
P00>>>show config

    Bus 00  Slot 08: DEC PCI MC                         mca0.0.0.8.0        Rev: 22, mca0

    Bus 01  Slot 03: DEC PCI MC                         mca1.1.0.3.0        Rev: 22, mca1
```
```