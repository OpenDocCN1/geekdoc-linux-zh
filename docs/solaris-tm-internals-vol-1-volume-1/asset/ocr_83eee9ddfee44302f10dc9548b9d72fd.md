routines for specific initialization steps, then returns to the common code to complete the boot process.

The platform-specific `startup()` function does some preliminary memory initialization: determining available physical memory after the core kernel is loaded, setting up of the kernel address space symbols, and allocating memory page structure. The kernel memory allocation (KVM) subsystem and the kstat (kernel statistics) framework, are initialized. Once these steps are completed, the operating system banner is displayed on the console;

```
SunOS Release 5.7 Version Generic 64-bit (UNIX(R) System V Release 4.0)
Copyright (c) 1983-1998, Sun Microsystems, Inc.
```

Additional platform-specific checking is done on processor types, firmware versions, etc., and the kernel `mod_read_system_file()` function is called to read the `/etc/system` file and populate internal data structures with the parameters and values set in `/etc/system`.

The kernel creates a linked list of `sysparam` data structures, such that each entry on the `/etc/system` file has a corresponding data structure in the list. The sysparam structure is defined in `/usr/include/sys/sysconf.h`, and is shown below.

```
/*
 * For each entry in /etc/system a sysparam record is created.
 */
struct sysparam {
        struct sysparam *sys_next; /* pointer to next */
        int     sys_type;          /* type for record */
        int     sys_op;            /* operation */
        char    *sys_modnam;       /* module name (null if param in kernel) */
        char    *sys_ptr;          /* string pointer to device, etc. */
        u_longlong_t sys_info;     /* additional information */
        char    *sys_conf;         /* configuration data */
        int     sys_len;            /* len of config data */
        u_long  *addrip;            /* pointer to value config addresses */
};
```

# Header File `<sys/sysconf.h>`

The fields in the sysparam structure are generally self-explanatory. Space is defined for parameter-specific information, the parameter type (e.g., a module load entry or an entry to set a value), and the necessary pointer to maintain the linked list. The `mod_read_sys_file()` code walks through each line on `/etc/system`, doing the necessary parsing to determine the entry types and setting the appropriate values in the sysparam structure that corresponds to the line entry in `/etc/system`. When `mod_read_sys_file()` is finished, a linked list of populated sysparam structures is established in kernel memory.

Before `mod_read_sys_file()` returns, the code sets the maxusers value. The maxusers parameter is calculated on the basis of the amount of physical memory