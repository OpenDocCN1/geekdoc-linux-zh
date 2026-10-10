
`module_param*` macros. These are explained in more detail in Chapter 8, “Device Driver Basics” when we introduce device drivers.

The new mechanism maintains backward compatibility by including an unknown function pointer argument in the parsing routine. Thus, parameters that are unknown to the `module_param*` infrastructure are considered unknown, and the processing falls back to the old mechanism under control of the developer. This is easily understood by examining the well-written code in `.../kernel/params.c` and the `parse_args()` calls in `.../init/main.c`.

The last point worth mentioning is the purpose of the `flag` member of the `obs_kernel_param` structure created by the `__setup` macro. Examination of the code in Listing 5-6 should make it clear. The `flag` in the structure, called early, is used to indicate whether this particular command line parameter was already consumed earlier in the boot process. Some command line parameters are intended for consumption very early in the boot process, and this `flag` provides a mechanism for an early parsing algorithm. You will find a function in `main.c` called `do_early_param()` that traverses the linker-generated array of `__setup`-generated structures and processes each one marked for early consumption. This gives the developer some control over when in the boot process this processing is done.

### 5.4 Subsystem Initialization

Many kernel subsystems are initialized by the code found in `main.c`. Some are initialized explicitly, as with the calls to `init_timers()` and `console_init()`, which need to be called very early. Others are initialized using a technique very similar to that described earlier for the `__setup` macro. In short, the linker builds lists of function pointers to various initialization routines, and a simple loop is used to execute each in turn. Listing 5-7 shows how this works.

#### Listing 5-7

**Example Initialization Routine**

```c
static int __init customize_machine(void)
{
    /* customizes platform devices, or adds new ones */
    if (init_machine)
        init_machine();
    return 0;
}
arch_initcall(customize_machine);
```

This code snippet comes from .../arch/arm/kernel/setup.c. It is a simple routine designed to provide a customization hook for a particular board.

#### 5.4.1 The `__initcall` Macros

Notice two important things about the initialization routine in Listing 5-7. First, it is defined with the `__init` macro. As we saw earlier, this macro applies the section attribute to declare that this function gets placed into a section called `.init.text` in the vmlinux ELF file. Recall that the purpose of placing this function into a special section of the object file is so the memory space that it occupies can be reclaimed when it is no longer needed.

The second thing to notice is the macro immediately following the definition of the function: `arch_initcall(customize_machine)`. This macro is part of a family of macros defined in .../include/linux/init.h. These macros are reproduced here as Listing 5-8.

#### Listing 5-8

**initcall Family of Macros**

```c
#define __define_initcall(level,fn) \
static initcall_t __initcall_##fn __attribute_used__ \
__attribute__("__section__(".initcall" level ".init")) = fn

#define core_initcall(fn)             __define_initcall(1,fn)
#define postcore_initcall(fn)         __define_initcall(2,fn)
#define arch_initcall(fn)             __define_initcall(3,fn)
#define subsys_initcall(fn)           __define_initcall(4,fn)
#define fs_initcall(fn)               __define_initcall(5,fn)
#define device_initcall(fn)           __define_initcall(6,fn)
#define late_initcall(fn)             __define_initcall(7,fn)
```

In a similar fashion to the `__setup` macro previously detailed, these macros declare a data item based on the name of the function, and use the section attribute to place this data item into a uniquely named section of the vmlinux ELF file. The benefit of this approach is that main.c can call an arbitrary initialization function for a subsystem that it has no knowledge of. The only other option, as mentioned earlier, is to pollute main.c with knowledge of every subsystem in the kernel.

As you can see from Listing 5-8, the name of the section is `.initcallN.init`, where N is the level defined between 1 and 7. The data item is assigned the address of the function being named in the macro. In the example defined by Listings 5-7 and 5-8, the data item would be as follows (simplified by omitting the section attribute):

```c
static initcall_t __initcall_customize_machine = customize_machine;
```

This data item is placed in the kernel’s object file in a section called `__initcall_init`. The level (N) is used to provide an ordering of initialization calls. Functions declared using the `core_initcall()` macro are called before all others. Functions declared using the `postcore_initcall()` macro are called next, and so on, while those declared with `late_initcall()` are the last initialization functions to be called.

In a fashion similar to the `__setup` macro, you can think of this family of `*_initcall` macros as registration functions for kernel subsystem initialization routines that need to be run once at kernel startup and then never used again. These macros provide a mechanism for causing the initialization routine to be executed during system startup, and a mechanism to discard the code and reclaim the memory after the routine has been executed. The developer is also provided up to seven levels of when to perform the initialization routines. Therefore, if you have a subsystem that relies on another being available, you can enforce this ordering using these levels. If you grep the kernel for the string `[a-z]*_initcall`, you will see that this family of macros is used extensively.

One final note about the `*_initcall` family of macros: The use of multiple levels was introduced during the development of the 2.6 kernel series. Earlier kernel versions used the `__initcall()` macro for this purpose. This macro is still in widespread use, especially in device drivers. To maintain backward compatibility, this macro has been defined to `device_initcall()`, which has been defined as a level 6 initcall.

### 5.5 The init Thread

The code found in `.../init/main.c` is responsible for bringing the kernel to life. After `start_kernel()` performs some basic kernel initialization, calling early initialization functions explicitly by name, the very first kernel thread is spawned. This thread eventually becomes the kernel thread called `init()`, with a process id (PID) of 1. As you will learn, `init()` becomes the parent of all Linux processes in user space. At this point in the boot sequence, two distinct threads are running: that represented by `start_kernel()` and now `init()`. The former goes on to become the idle process, having completed its work. The latter becomes the init process. This can be seen in Listing 5-9.

#### Listing 5-9. Creating Kernel init Thread

```c
static void __init init (void)
{ 
    static struct kernel_lock task_lock;
    static int count;

    release_kernel_lock;

    kernel_thread(init, NULL, CLONE_FS | CLONE_FILES);

    num_dequeueable_policies();

    unlock_kernel_lock();
    preempt_enable_no_resched();
}
```

To remind you of what we discussed above, the value of the stack in Listing 5-8 shows that we are currently in the context of an interrupt handler. When the interrupt ends, control is passed to `schedule()`, which eventually switches to a different process. The process that is executed next might or might not have an associated stack. If it does, that stack will be set up by the kernel. This happens, for example, with the start of the process that was created by the call to `kernel_thread()` inside `init()`. This process is called pid 1. It is created by the call to `kernel_thread()` in `init()`. This call is in the context of an interrupt handler. When the interrupt ends, control is passed to `schedule()`, which eventually switches to a different process. The process that is executed next might or might not have an associated stack. If it does, that stack will be set up by the kernel. This happens, for example, with the start of the process that was created by the call to `kernel_thread()` in `init()`.

The `start_kernel()` function calls `rest_init()`, reproduced in Listing 5-9. The kernel's init process is spawned by the call to `kernel_thread()`. `init()` goes on to complete the rest of the system initialization, while the thread of execution started by `start_kernel()` loops forever in the call to `cpu_idle()`.

The reason for this structure is interesting. You might have noticed that `start_kernel()`, a relatively large function, was marked with the `__init` macro. This means that the memory it occupies will be reclaimed during the final stages of kernel initialization. It is necessary to exit this function and the address space it occupies before reclaiming its memory. The answer to this was for `start_kernel()` to call `rest_init()`, shown in Listing 5-9, a much smaller piece of memory that becomes the idle process.
