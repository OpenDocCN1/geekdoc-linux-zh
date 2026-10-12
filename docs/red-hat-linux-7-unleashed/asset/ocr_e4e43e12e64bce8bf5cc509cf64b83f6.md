# Resolving IRQs and Memory Ports

If you have IRQ and/or memory conflicts, and if you have a Windows partition, you can find the values used by Windows in the Control Panel, System, Devices listings and then use these settings on the li1o command line, in /etc/ modules.conf, or in your BIOS PnP settings. It is unfortunate, but a few manu- facturers still believe their best business model is to restrict use of their hard- ware to Microsoft users. When techniques and interfaces for probing and configuring these devices are not available to Linux programmers, we are forced to reverse engineer the protocols, which can sometimes result in a lack of Linux support until after the device is obsolete. Fortunately, most manufac- turers have seen the light and happily provide the information needed to incor- porate their products under Linux.

# Kernel Panic

A kernel panic message has a certain cryptic poetry to it, like a robotic haiku, a snapshot testament to the last moments of a Linux kernel. A kernel panic usually has the following form:

```
```
unable to handle kernel paging request at address C0000010
Oops: 0002
EIP: 0010:XXXXXX
   eax: xxxxxxxx ebx: xxxxxxxx ecx: xxxxxxxx edx: xxxxxxxx
   esi: xxxxxxxx edi: xxxxxxxx ebp: xxxxxxxx
   ds: xxxx es: xxxx fs: xxxx gs: xxxx
Pid: xx, process nr: xx

xx xx xx xx xx xx xx xx xx xx
```
```

For most practical purposes, knowing where the panic occurs is more useful than interpret- ing the message itself. The leading text tells what triggered the event, and this is followed by the addresses held in various registers. Intrepid readers can find detailed instructions on decoding this message in the 1inux/Documentation/oops-tracing.txt file.

In production kernels, panic messages are rare and are usually due to a misconfiguration problem, missing modules, failure to load a module before using some essential feature, or using hardware not supported by the current kernel. With development kernels, kernel panics can become a way of life.