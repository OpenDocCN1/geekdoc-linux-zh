# Configuring Your Kernel

When configuring your kernel, the number of options might seem overwhelming at first. However, for a routing machine there is a fairly small subset of functions and devices that you'll need to worry about; the rest can safely be disabled. For instance, you're almost certainly not going to need support for telephony or Ham radio in a routing machine.

In this section we'll cover the options that you will want to deal with. We're looking specifically at the 2.4 kernel, but most of these options do apply to the 2.2.x kernel series as well.

By the way, it's worth noting that there might be additional hardware support or functionality in the kernel by the time that you read this. We aren't aware of any planned additions for the kernel at the time of this writing, but that's not to say that it's unlikely.

# Code Maturity Level Options

Several of the new networking functions in the Linux kernel are still considered "experimental." Selecting the Prompt for Development and/or Incomplete Code/Drivers option will simply give you the option of selecting these options when configuring the rest of the kernel. Selecting this option, in and of itself, won't add any "experimental" code to your kernel, make it unstable in any way, or increase the size of the compiled kernel. It's probably a good idea to say yes to this option.

# Processor Type and Features

This option is mostly specific to Intel-based hardware. You can choose the type of processor that you're using in your router to optimize the kernel for that machine. Note that if you compile a kernel for a specific processor, such as the "PPro/6x86MX Processor Family," it might not boot on other processors. If you choose this option, you might wish to compile a "generic" kernel with the same options in case you have to swap motherboards and processors in the machine at a later date.

If the routing machine is a dual-processor, you also will want to enable symmetric multi-processing (SMP) support in the kernel

The Math emulation and MTRR (Memory Type Range Register) support shouldn't be necessary for a routing machine. Any recent CPU (486 and up) will already have a math co-processor and won't require math emulation.

# Loadable Module Support

As the name implies, selecting this option will allow you to compile module support into the kernel. Naturally, this option is one of the kernel options not available as a module, for obvious reasons.