
## D.3 SDRAM Setup

```c
34 mtsdram0(mem_edtrl, edtr1);
35 mtsdram0(mem_rtr, rtr);
36
37 udelay(200);
38
39 /*
40 * Set memory controller options reg, MCOPT1.
41 * Set DC_EN to '1', and BRD_PRF to '01' for 16 byte PLB
42 * Burst read/prefetch.
43 */
44 mtsdram0(mem_mcopt1, 0x80800000);
45 udelay(100000);
46
47 if (get_ram_size(0, 0, mb0cf[1].size) == mb0cf[1].size) {
48     /* OK, size detected -> all done */
49     return;
50 }
51
52 }
```

The first action reads the pin strapping on the 405GP processor to determine the design value for the SDRAM clock. In this case, we can see that two possible values are accommodated: 100MHz and 133MHz. Based on this choice, constants are chosen that will be used later in the function to set the appropriate register bits in the SDRAM controller.

Starting on line 24, a loop is used to set the parameters for each of up to five pre-defined memory sizes. Currently, U-Boot has logic to support a single bank of memory sized at 4MB, 16MB, 32MB, 64MB, or 128MB. These sizes are defined in a table called `mb0cf` in .../cpu/ppc4xx/sdram.c. The table associates a constant with each of these memory sizes, based on the value required in the 405GP memory bank configuration register. The loop does this:

```c
for (i = each possible memory bank size, largest first) {
    select timing constant based on SDRAM clock speed;
    disable SDRAM memory controller;
    configure bank 0 with size[i], timing constants[i];
    enable SDRAM memory controller;
    run simple memory test to dynamically determine size;
    /* This is done using get_ram_size() */
    if ( tested size == configured size )
        done;
}
```

This simple logic simply plugs in the correct timing constants in the SDRAM controller based on SDRAM clock speed and configured memory bank size from the hard-coded table in U-Boot. Using this explanation, you can easily correlate the bank configuration values using the 405GP reference manual. For a 64MB DRAM size, the memory bank control register is set as follows:

```
Memory Bank 0 Control Register = 0x000a4001
```

The PowerPC 405GP User's Manual describes the fields in Table D-2 for the memory bank 0 control register.

### TABLE D-2
405GP Memory Bank 0-3 Configuration Register Fields

| Field | Value | Comments |
| :--- | :--- | :--- |
| Bank Address (BA) | 0x00 | Starting memory address of this bank. |
| Size (SZ) | 0x4 | Size of this memory bank—in this case, 64MB. |
| Addressing Mode (AM) | 0x2 | Determines the organization of memory, including the number of row and column bits. In this case, Mode 2 = 12 row address bits, and either 9 or 10 column address bits, and up to four internal SDRAM banks. This data is provided in a table in the 405GP user's manual. |
| Bank Enable (BE) | 0x1 | Enable bit for the bank configured by this register. There are four of these memory bank configuration registers in the 405GP. |

The values in this table must be determined by the designer, based on the choice of memory module in use on the board.

Let's look at a timing example for more detail on the timing requirements of a typical SDRAM controller. Assuming a 100MHz SDRAM clock speed and 64MB memory size, the timing constants selected by the `sdram_init()` function in Listing D-1 are selected as follows:

```
SDRAM Timing Register = 0x36346884
Refresh Timing Register = 0x35200000
```

The PowerPC 405GP User's Manual describes the fields in Table D-3 for the SDRAM Timing Register.

### TABLE D-3
405GP SDRAM Timing Register Fields

| Field | Value | Comments |
| :--- | :--- | :--- |
| CAS Latency (CASL) | 0x1 | SDRAM CAS Latency. This value comes directly from the SDRAM chip specifications. It is the delay in clock cycles required by the chip between issuance of the read command (CAS signal) until the data is available on the data bus. In this case, the 0x1 represents two clock cycles, as seen from the 405GP user's manual. |
| Precharge Command to Next Activate (PTA) | 0x1 | The SDRAM Precharge command deactivates a given row. In contrast, the Activate command enables a given row for subsequent access, such as during a burst cycle. This timing parameter enforces the minimum time between Precharge to a subsequent Activate cycle and is dictated by the SDRAM chip. The correct value must be obtained from the SDRAM chip specification. In this case, 0x1 represents two clock cycles, as determined from the 405GP user's manual. |
| Read/Write to Precharge Command Minimum (CTP) | 0x2 | This timing parameter enforces the minimum time delay between a given SDRAM read or write command to a subsequent Precharge command. The correct value must be obtained from the SDRAM chip specification. In this case, 0x2 represents three clock cycles, as determined from the 405GP user's manual. |
| SDRAM Command Leadoff (LDF) | 0x1 | This timing parameter enforces the minimum time delay between assertion of address or command cycle to bank select cycle. The correct value must be obtained from the SDRAM chip specification. In this case, 0x1 represents two clock cycles, as determined from the 405GP user's manual. |

The final timing parameter configured by the U-Boot example in Listing D-1 is the refresh timing register value. This register requires a single field that determines the refresh interval enforced by the SDRAM controller. The field representing the interval is treated as a simple counter running at the SDRAM clock frequency. In the example here, we assumed 100MHz as the SDRAM clock frequency. The value programmed into this register in our example is 0x05f0_0000. From the PowerPC 405GP User’s Manual, we determine that this will produce a refresh request every 15.2 microseconds. As with the other timing parameters, this value is dictated by the SDRAM chip specifications.

A typical SDRAM chip requires one refresh cycle for each row. Each row must be refreshed in the minimum time specified by the manufacturer. In the chip referenced in Section D.4.1, “Suggestions for Additional Reading,” the manufacturer specifies that 8,192 rows must be refreshed every 64 milliseconds. This requires generating a refresh cycle every 7.8 microseconds to meet the specifications for this particular device.

## D.4 Summary

SDRAM devices are quite complex. This appendix presented a very simple example to help you navigate the complexities of SDRAM controller setup. The SDRAM controllers perform a critical function and must be properly set up. There is no substitute to diving into a specification and digesting the information presented. The two example documents referenced in this appendix are excellent starting points.

### D.4.1 Suggestions for Additional Reading

- AMCC 405GP Embedded Processor User’s Manual
  - AMCC Corporation
  - www.amcc.com/Embedded/

- Micron Technology, Inc.
  - Synchronous DRAM MT48LC64M4A2 Data Sheet
  - http://download.micron.com/pdf/datasheets/dram/sdram/256MSDRAM.pdf

# Appendix E

![](img/7a1144833e62564667e7dd9eb4c9f03d_532_0.png)

## Source Repositories and Developer Information

Several locations on the Web focus on Linux development. Here is a list of the most important websites for the various architectures and projects:

- Primary kernel source tree
  - www.kernel.org
- Primary kernel GIT repository
  - www.kernel.org/git
- PowerPC-related development and mailing lists
  - http://ozlabs.org/
- MIPS-related developments
  - www.linux-mips.org
- ARM-related Linux development
  - www.arm.linux.org.uk
- Primary home for a huge collection of open-source projects
  - http://sourceforge.net

## Mailing Lists

Hundreds, if not thousands, of mailing lists cater to every aspect of Linux and open-source development. Here are a few to consider. Make sure you familiarize yourself with mailing list etiquette before posting to these lists.

Most of these lists maintain archives that are searchable. This is the first place that you should consult. In a great majority of the cases, your question has already been asked and answered. Start your reading here, for advice on how to best use the public mail lists:

- The Linux Kernel Mailing List FAQ
  - www.rux.org/lkml
- List server serving various Linux kernel-related mail lists
  - http://vger.kernel.org
- Linux Kernel Mailing--very high volume, kernel development only
  - http://vger.kernel.org/vger-lists.html#linux-kernel
