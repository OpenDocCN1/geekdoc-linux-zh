| FIONBIO | 0x5421 | set/reset O_NONBLOCK from arg; |
| FIONCLEX | 0x5450 | clear close-on-exec flag; |
| FIOCLEX | 0x5451 | set close-on-exec flag; |
| FIOASYNC | 0x5452 | set/reset O_SYNC from arg. |

If you use any of these four cmd values for your own ioctl() commands then your routines will never be called because the kernel gets to them first.

# 25.5 Interrupts

In addition to the functions accessed via the file_operations structure, a device driver can also supply an interrupt() service routine. This will only be required where there is underlying hardware involved, capable of generating an interrupt signal.

In much the same way as you need to register your device driver with the kernel so that access to device special files with your major device number will call your driver's routines, you also need to request that the kernel associates a particular interrupt request line (IRQ) with your interrupt service routine, so that when the interrupt occurs, your routine will get called. This is done with the request_irq() function:

```
#include <linux/signal.h>
```

```
int request_irq(unsigned int irq, void (*handler)(int),
    unsigned long type, char *name);
```

where irq is the interrupt (IRQ) number you are trying to register, handler is a pointer to the interrupt service routine, type is a flag which specifies whether this should be a normal or fast interrupt, and name is the name of your device driver.

The difference between a normal and fast interrupt is that, on return from executing a normal interrupt routine, the kernel can take the opportunity to run the scheduler (via a call to the kernel schedule() function) to see if there is a more appropriate process to execute than the current one. If there is, then the current process will be preempted and the new process will run instead. In the case of a fast interrupt this scheduling is not performed so that the interrupted process will be resumed when the interrupt service routine returns.

The values for type are zero for normal interrupts and the symbolic constant SA_INTERRUPT for fast interrupts.

Interrupt handlers can also be un-registered by use of the free_irq() function:

```
void free_irq(unsigned int irq);
```

where irq is the IRQ number to free.