| If Storage Class is | And Variable is declared | Then it can be referenced | And can be initialized with | Comments |
| :--- | :--- | :--- | :--- | :--- |
| *static* | Outside any BLOCK | Anywhere within the file | Constant expression only | Variables are initialized only once at the start of program execution; values are retained through BLOCKS; default value is 0. |
| | Inside a BLOCK | Within the BLOCK | | |
| *extern* | Outside any BLOCK | Anywhere within the file | Constant expression only | Variable must be declared in at least one place without the `extern` keyword, or in one place using the keyword `extern` and assigned an initial value. |
| | Inside a BLOCK | Within the BLOCK | | |
| *auto* | Inside a BLOCK | Within the BLOCK | Any valid expression | Variable is initialized each time the BLOCK is entered; no default value. |
| *register* | Inside a BLOCK | Within the BLOCK | Any valid expression | Assignment to register not guaranteed; varying restrictions on types of variables that can be declared; cannot take the address of a register variable; initialized each time BLOCK is entered; no default value. |
| *omitted* | Outside any BLOCK | Anywhere within the file or by other files that contain appropriate declarations | Constant expressions only | This declaration can appear in only one place; variable is initialized at the start of program execution; default value is 0; defaults to `auto`. |
| | Inside a BLOCK | (See *auto*) | (See *auto*) | |
| **Table A.6** | **Variables: Summary of Storage Classes, Scope, and Initialization** | | | |

# ## 7.0 Functions

This section summarizes the syntax and operation of functions.

# ## 7.1 Function Definition

The general format for declaring a function definition is as follows:

Click here to view code image