
RAM; and a proper context can be constructed to run higher-level languages such as C. This allows the rest of the processor and platform initialization to be written in something other than assembly language.

## 7.3 A Universal Bootloader: Das U-Boot

Many open-source and commercial bootloaders are available, and many more one-off home-grown designs are in widespread use today. Most of these have some level of commonality of features. For example, all of them have some capability to load and execute other programs, particularly an operating system. Most interact with the user through a serial port. Support for various networking subsystems (such as Ethernet) is less common but a very powerful feature.

Many bootloaders are specific to a particular architecture. The capability of a bootloader to support a wide variety of architectures and processors can be an important feature to larger development organizations. It is not uncommon for a single development organization to have multiple processors spanning more than one architecture. Investing in a single bootloader across multiple platforms ultimately results in lower development costs.

In this section, we study an existing bootloader that has become very popular in the embedded Linux community. The official name for this bootloader is Das U-Boot. It is maintained by Wolfgang Denk and hosted on SourceForge at http://u-boot.sourceforge.net/. U-Boot has support for multiple architectures and has a large following of embedded developers and hardware manufacturers who have adopted it for use in their projects and have contributed to its development.

### 7.3.1 System Configuration: U-Boot

For a bootloader to be useful across many processors and architectures, some method of configuring the bootloader is necessary. As with the Linux kernel itself, configuration of a bootloader is done at compile time. This method significantly reduces the complexity of the bootloader, which, in itself, is an important characteristic.

In the case of U-Boot, board-specific configuration is driven by a single header file specific to the target platform, and a few soft links in the source tree that select the correct subdirectories based on target board, architecture, and CPU. When configuring U-Boot for one of its supported platforms, issue this command:

```
$ make <platform>_config
```

Here, platform is one of the many platforms supported by U-Boot. These platform-configuration targets are listed in the top level U-Boot makefile. For example, to configure for the Spectrum Digital OSK, which contains a TI OMAP 5912 processor, issue this command:

```
$ make omap5912osk_config
```

This configures the U-Boot source tree with the appropriate soft links to select ARM as the target architecture, the ARM926 core, and the 5912 OSK as the target platform.

The next step in configuring U-Boot for this platform is to edit the configuration file specific to this board. This file is found in the U-Boot `../include/configs` subdirectory and is called *omap5912osk.h*. The README file that comes with the U-Boot distribution describes the details of configuration and is the best source for this information.

Configuration of U-Boot is done using configuration variables defined in a board-specific header file. Configuration variables have two forms. Configuration *options* are selected using macros in the form of `CONFIG_XXXX`. Configuration *settings* are selected using macros in the form of `CFG_XXX`. In general, configuration options (`CONFIG_XXX`) are user configurable and enable specific U-Boot operational features. Configuration settings (`CFG_XXX`) are usually hardware specific and require detailed knowledge of the underlying processor and/or hardware platform. Board-specific U-Boot configuration is driven by a header file dedicated to that specific platform that contains configuration options and settings appropriate for the underlying platform. The U-Boot source tree includes a directory where these board-specific configuration header files reside. They can be found in `../include/configs` from the top-level U-Boot source directory.

Numerous features and modes of operation can be selected by adding definitions to the board-configuration file. Listing 7-4 contains a partial configuration header file for a fictitious board based on the PPC 405GP processor.

**Listing 7-4**

**Partial U-Boot Board-Configuration Header File**

```c
#define CONFIG_405GP     /* Processor definition */
#define CONFIG_4XX     /* Sub-arch specification, 4xx family */

#define CONFIG_SYS_CLK_FREQ  33333333  /* PLL Frequency */
#define CONFIG_BAUDRATE      9600
#define CONFIG_PCI     /* Enable support for PCI */
...
#define CONFIG_COMMANDS     (CONFIG_CMD_DFL | CFG_CMD_DHCP)
...
#define CFG_BASE_BAUD      691200

/* The following table includes the supported baudrates */
#define CFG_BAUDRATE_TABLE \
 (1200, 2400, 4800, 9600, 19200, 38400, 57600, 115200, 230400)

#define CFG_LOAD_ADDR      0x100000  /* default load address */
...
/* Memory Bank 0 (Flash Bank 0) initialization */
#define CFG_EBC_PB0AP      0x9B015480
#define CFG_EBC_PB0CR      0xFFF18000

#define CFG_EBC_PB1AP      0x02815480
#define CFG_EBC_PB1CR      0xFFF018000
...
```

Listing 7-4 gives an idea of how U-Boot itself is configured for a given board. An actual board-configuration file can contain hundreds of lines similar to those found here. In this example, you can see the definitions for the CPU, CPU family (4xx), PLL clock frequency, serial port baud rate, and PCI support. We have included examples of configuration variables (`CONFIG_XXX`) and configuration settings (`CFG_XXX`). The last few lines are actual processor register values required to initialize the external bus controller for memory banks 0 and 1. You can see that these values can come only from a detailed knowledge of the board and processor.

Many aspects of U-Boot can be configured using these mechanisms, including what functionality will be compiled into U-Boot (support for DHCP, memory tests, debugging support, and so on). This mechanism can be used to tell U-Boot how much and what kind of memory is on a given board, and where that memory is mapped. The interested reader can learn much more by looking at the U-Boot code directly, especially the excellent README file.

### 7.3.2 U-Boot Command Sets

U-Boot supports more than 60 standard command sets that enable more than 150 unique commands using `CFG_*` macros. A command set is enabled in U-Boot through the use of configuration setting (`CFG_*`) macros. For a complete list from a recent U-Boot snapshot, consult Appendix B, “U-Boot Configurable Commands.” Here are just a few, to give you an idea of the capabilities available:

| Command Set       | Commands                                          |
| ----------------- | ------------------------------------------------- |
| `CFG_CMD_FLASH`   | Flash memory commands                              |
| `CFG_CMD_MEMORY`  | Memory dump, fill, copy, compare, and so on       |
| `CFG_CMD_DHCP`    | DHCP Support                                        |
| `CFG_CMD_PING`    | Ping support                                        |
| `CFG_CMD_EXT2`    | EXT2 File system support                            |

The following line of Listing 7-4 defines the commands enabled in a given U-Boot configuration, as driven by the board-specific header file:

```
#define CONFIG_COMMANDS (CONFIG_CMD_DFL | CFG_CMD_DHCP)
```

Instead of typing out each individual `CFG_*` macro in your own board-specific configuration header, you can start from a default set of commands predefined in the U-Boot source. The macro `CONFIG_CMD_DFL` defines this default set of commands. `CONFIG_CMD_DFL` specifies a list of default U-Boot command sets such as `tftpboot` (boot an image from a tftpserver), `bootm` (boot an image from memory), memory utilities such as `md` (display memory), and so on. To enable your specific combination of commands, you can start with the default and add and subtract as necessary. The example from Listing 7-4 adds the DHCP command set to the default. You can subtract in a similar fashion:

```
#define CONFIG_COMMANDS (CONFIG_CMD_DFL & ~CFG_CMD_NFS)
```

Take a look at any board-configuration header file in `../include/configs/` for examples.

### 7.3.3 Network Operations

Many bootloaders include support for Ethernet interfaces. In a development environment, this is a huge time saver. Loading even a modest kernel image over a serial
