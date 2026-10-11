**Table 22.1 Commonly used preprocessor options available for gcc (continued).**

| Option | Purpose | Value | Example |
| :--- | :--- | :--- | :--- |
| **-MD** | Outputs statements that can be used for building a Makefile for this program, but saves the dependency information to a file with a .d extension so as to not interfere with the remaining compilation steps | None | **-MD** |
| **-MMD** | Outputs statements that can be used for building a Makefile for this program, but saves the dependency information to a file with a .d extension so as to not interfere with the remaining compilation steps; ignores system header files | None | **-MMD** |
| **-nostdinc** | Ignores system header directories | None | **-nostdinc** |
| **-trigraphs** | Ensures that standard C code is outputted, though this is often undesirable because of its strict nature | None | **-trigraphs** |
| **-U** | Undefines the specified macro | Macro name | **-Uthree** |
| **-undef** | Specifies that no macros should be defined unless specifically done so in the code | None | **-undef** |
| **-Wp,** | Passes a specific option— or more than one—to the preprocessor | Option(s), comma-separated if more than one | **-Wp,-MG** |

**Table 22.2 Options for use when only preprocessing with gcc.**

| Option | Purpose |
| :--- | :--- |
| **-C** | Leaves comments intact |
| **-dM** | Outputs only the macro definitions that have been set when preprocessing is finished |
| **-M** | Outputs statements that can be used for building a Makefile for this program |
| **-MG** | Outputs statements that can be used for building a Makefile for this program, assuming that the header files are in the same location as the source files |