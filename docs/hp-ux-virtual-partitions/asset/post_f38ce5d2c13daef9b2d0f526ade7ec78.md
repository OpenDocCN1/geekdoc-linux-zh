
## isl - Initial System Loader (isl) overview

**isl(1M)**  
**Series 800 Com**  
**isl(1M)**

### NAME

isl - initial system loader

### DESCRIPTION

isl implements the operating system independent portion of the bootstrap process. It is loaded and executed after self-test and initialization have completed successfully.

The processor contains special purpose memory for maintaining critical configuration related parameters (e.g. Primary Boot, Alternate Boot, and Console Paths). Two forms of memory are supported: Stable Storage and Non-Volatile Memory (NVM).

**Typically, when control is transferred to isl, an autoboot sequence takes place.** An autoboot sequence allows a complete bootstrap operation to occur with no intervention from an operator. isl executes commands from the autoboot file in a script-like fashion. autoboot is enabled by a flag in Stable Storage.

autosearch is a mechanism that automatically locates the boot and console devices. For further information, see ldc(1M).

During an autoboot sequence, isl displays its revision and the name of any utility it executes. However, if autoboot is disabled, after isl displays its revision, it then prompts for input from the console device. Acceptable input is any isl command name or the name of any utility available on the system. If a non-fatal error occurs or the executed utility returns, isl again prompts for input.

### Commands

There are several commands available in isl. The following is a list with a short description. Parameters may be entered on the command line following the command name. They must be separated by spaces. isl prompts for any necessary parameters that are not entered on the command line.

1. **? help** - List commands and available utilities
2. **lsrcl** - List available utilities
3. **ls** - List available utilities
4. **autoboot** - Enable or disable the autoboot sequence; Parameter - on or off
5. **autosearch** - Enable or disable the autosearch sequence; Parameter - on or off
6. **primpath** - Modify the Primary Boot Path; Parameter - Primary Boot Path in decimal
7. **altPath** - Modify the Alternate Boot Path; Parameter – Alternate Boot Path in decimal
8. **conpath** - Modify the Console Path; Parameter – Console Path in decimal
9. **isauto1** - List contents of the autoexecute file
10. **display** - Display the Primary Boot, Alternate Boot, and Console Paths
11. **readnm** - Display the contents of one word of NVM in hexadecimal; Parameter – NVM address in decimal or standard hexadecimal notation
12. **readss** - Display the contents of one word of Stable Storage in hexadecimal; Parameter – Stable Storage address in decimal or standard hexadecimal notation

### DIAGNOSTICS

isl displays diagnostic information through error messages written on the console and display codes on the LED display.

For the display codes, CEQX are informative only. CYKX and CY2X indicate errors, some of which are fatal and cause the system to halt. Other errors merely cause isl to display a message.

Non-fatal errors during an autoboot sequence cause the autoboot sequence to be aborted and isl to prompt for input. After non-fatal errors during an interactive isl session, isl merely prompts for input.

Fatal errors cause the system to halt. The problem must be corrected and the system RESET to recover.

- **CE00** isl is executing.
- **CE01** isl is autobooting from the autoexecute file.
- **CE02** Cannot find an autoexecute file, autoboot aborted.
- **CE03** No console found, isl can only autoboot.
- **CE05** Directory of utilities is too big, isl reads only 2K bytes.
- **CE06** autoexecute file is inconsistent, autoboot aborted.
- **CE07** Utility file header inconsistent: COW values invalid.
- **CE08** autoexecute file input string exceeds 2048 characters, autoboot aborted.
- **CE09** isl command or utility name exceeds 10 characters.
- **CE10** isl has transferred control to the utility.
- **CE11** Internal inconsistency: Volume label - FATAL.
- **CE12** Internal inconsistency: Directory - FATAL.
- **CE13** Error reading autoexecute file
- **CE14** Error reading from console - FATAL.
- **CE15** Error writing to console - FATAL.
- **CE16** Not an isl command or utility.
- **CE17** Utility file header inconsistent: Invalid System ID.
- **CE18** Utility file header inconsistent: Bad magic number.
- **CE19** Utility would overwlay isl in memory.
- **CE1A** Utility requires more memory than is configured.
- **CE1B** Error reading utility into memory.
- **CE1C** Error reading utility into memory.
- **CE1D** Incorrect checksum: Reading utility into memory.
- **CE1E** Console needed - FATAL.
- **CE1F** Internal inconsistency: Boot device class - FATAL.
- **CE21** Destination memory address of utility is invalid.
- **CZ22** Utility file header inconsistent: pdc cache entry.
- **CZ23** Internal inconsistency: iode_entry_init - FATAL.
- **CZ24** Internal inconsistency: iode_entry_init - console - FATAL.
- **CZ25** Internal inconsistency: iode_entry_init - boot device - FATAL.
- **CZ26** Utility file header inconsistent: Bad aux id.
- **CZ27** Bad utility file type.

### SEE ALSO

boot(1M), hpx_800(1M), pdc(1M).

## pdc

![](img/eff8b9287a5f38c5adf538f24aacf29e_221_0.png)

### pdc - Processor Dependent Code (pdc) overview

**pdc(1M)**

### NAME

pdc - processor-dependent code (firmware)

### DESCRIPTION

pdc is the firmware that implements all processor-dependent functionality, including initialization and self-test of the processor. Upon completion, it loads and transfers control to the initial system loader (isl(1M)). Firmware behavior varies somewhat, depending on the hardware series as described below.

- **Series 800 Behavior**
  - To load isl from an external medium, pdc must know the particular device on which isl resides. Typically the device is identified by the Primary Boot Path that is maintained by pdc in Stable Storage. A path specification is a series of decimal numbers each suffixed by `/`, indicating bus converters, followed by a series of decimal numbers separated by `,`, indicating the various card and slot numbers and addresses. The first number, not specifying a bus converter, is the MID-BUS module number (that is, slot number times four) and followed by the CIO slot number. If the CIO slot contains an EP-TB card, the next number is the HP-IB address, followed by the unit number of the device if the device supports units. If the CIO slot contains a terminal card, the next number is the port number, which must be zero for the console.
  - When the processor is reset after initialization and self-test complete, pdc reads the Console Path from Stable Storage, and attempts to initialize the console device. If the initialization fails, pdc attempts to find and initialize a console device. Algorithms used to find a console device are model-dependent. pdc then announces the Primary Boot, Alternate Boot, and Console Paths.
  - If autoboot (see isl(1M)) is enabled, pdc provides a 10-second delay, during which time the operator can override the autoboot sequence by typing any character on the console. If the operator does not interrupt this process, pdc initializes and reads isl from the Primary Boot Path. On models that support autoboot, if this path is not valid and autosearch (see isl(1M)) is enabled, pdc then searches through the MID-BUS modules and CIO slots to find a bootable medium. Currently, autosearch is only implemented on the model 825.
  - If the autoboot sequence is unsuccessful, overridden by the operator, or not enabled in the first place, pdc interactively prompts the operator for the Boot Path to use. Any required path components that are not supplied default to zero.
  - The Primary Boot, Alternate Boot, and Console Paths as well as autoboot and autosearch enable can be modified via isl.
- **Series 700 Behavior**
  - To load isl from an external medium, pdc must know the particular
