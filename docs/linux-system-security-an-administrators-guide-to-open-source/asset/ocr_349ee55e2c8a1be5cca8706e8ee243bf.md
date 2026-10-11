| Control Flag | Description |
|---|---|
| required | This module must return success for the service to be granted. If this module is one in a series of stacked modules, all other modules are still executed. The application will not be informed as to which module or modules failed. |
| requisite | As above, except that failure here terminates execution of all modules and immediately returns a failure status to the application. |
| optional | As the name implies, this module is not required. If it is the only module, however, its return status to an application may cause failure. |
| sufficient | If this module succeeds, all remaining modules in the stack are ignored and success is returned to the application. In particular, if the module succeeds, this means that no subsequent modules in the stack are executed, regardless of the control flags associated with the subsequent modules. If this module fails it does not necessarily cause failure of the stack, unless it is the only module in the stack. |

The arguments field is used for specifying flags or options that are passed to the module. Specifying arguments is optional. There are certain general arguments available for most modules which are listed in Table 5.3. Other arguments are available on a per-module basis and will be discussed appropriately with each module.

In summary, each file in /etc/pam.d is associated with the service or application after which the file is named and contains a list of records, each of which contains a module type, control flag, module name and location, and optional arguments. If the modules are of the same type, they are considered to be stacked and will be executed in the order in which they appear, unless control flags terminate execution earlier. The entire stack, not just one module,

| Standard Arguments | Description |
|---|---|
| debug | Generates additional output to the syslog utility. Most PAM modules support this argument. Its exact definition depends on the module to which this argument is supplied. |
| no_warn | Do not pass warning messages to the application. |
| use_first_pass | This module will use the password from the previous module. If it fails, no attempt is made to obtain another entry from the user. This argument is intended for auth and password modules only. |
| try_first_pass | As above, except that, if the password fails, it will prompt the user for another entry. This argument is intended for auth and password modules only. |

> The syslog utility is discussed in detail in Chapter 8.