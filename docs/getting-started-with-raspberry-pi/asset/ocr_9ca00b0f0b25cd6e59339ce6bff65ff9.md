# Looking at the Sources

In the 2.4 kernel source tree, a single directory (*drivers/i2c/*) contained all the I²C/SMBus-related sources. The I²C code in 2.6 kernels is organized hierarchically: The *drivers/i2c/busses/* directory contains adapter drivers, the *drivers/i2c/algos/* directory has algorithm drivers, and the *drivers/i2c/chips/* directory contains client drivers. You can find client drivers in other regions of the source tree, too. The *drivers/sound/* directory, for example, includes drivers for audio chipssets that use an I²C control interface. Take a look inside the *Documentation/i2c/* directory for tips and more examples.

Kernel SPI service functions live in *drivers/spi/spi.c*. The SPI driver for the ADS7846 touch controller is implemented in *drivers/input/touchscreen/ads7846.c*. The MTD subsystem discussed in Chapter 17, “Memory Technology Devices,” implements drivers for SPI flash chips. An example is *drivers/mtd/devices/mtd_dataflash.c*, the driver to access Atmel DataFlash SPI chips.

The *drivers/w1/* directory contains kernel support for the w1 protocol. Drivers for the host controller side of the w1 interface live in *drivers/w1/masters/*, and drivers for w1 slaves reside in *drivers/w1/slaves/*.

*Table 8.3* summarizes the main data structures used in this chapter and their location in the kernel tree. *Table 8.4* lists the main kernel programming interfaces that you used in this chapter along with the location of their definitions.

**Table 8.3. Summary of Data Structures**

| Data Structure | Location | Description |
|---|---|---|
| i2c_driver | include/linux/i2c.h | Representation of an I²C driver |
| i2c_client_address_data | include/linux/i2c.h | Slave addresses that an I²C client driver is responsible for |
| i2c_client | include/linux/i2c.h | Identifies a chip connected to an I²C bus |
| i2c_msg | include/linux/i2c.h | Information pertaining to a transaction that you want to generate on the I²C bus |
| spi_driver | include/linux/spi/spi.h | Representation of an SPI driver |
| spi_device | include/linux/spi/spi.h | Representation of an SPI device |
| spi_transfer | include/linux/spi/spi.h | Details of an SPI transfer buffer |
| spi_message | include/linux/spi/spi.h | Sequence of spi_transfer segments |
| w1_family | drivers/w1/w1_family.h | Representation of a w1 slave driver |
| w1_family_ops | drivers/w1/w1_family.h | A w1 slave driver’s entry points |

**Table 8.4. Summary of Kernel Programming Interfaces**