# Pseudo Char Drivers

Several commonly used kernel facilities are not connected with any physical hardware, and these are elegantly implemented as char devices. The $null$ sink, the perpetual $zero$ source, and the kernel random number generator are treated as virtual devices and are accessed using $pseudo$ char device drivers.

The $/dev/null$ char device sinks data that you don't want to display on your screen. So if you need to check out source files from a Concurrent Versioning System (CVS) repository without spewing filenames all over the screen, do this:

```
bash> cvs co kernel > /dev/null
```

This redirects command output to the write entry point belonging to the $/dev/null$ driver. The driver's $read()$ and $write()$ methods simply return success ignoring the contents of the input and output buffers, respectively.

If you want to fill an image file with zeros, call upon $/dev/zero$ to come to your service:

```
bash> dd if=/dev/zero of=file.img bs=1024 count=1024
```

This sources a stream of zeros from the $read()$ method belonging to the $/dev/zero$ driver. The driver has no $write()$ method.

The kernel has a built-in random number generator. For the benefit of kernel users who desire to use random sequences, the random number generator exports APIs such as $get_random_bytes()$. For user mode programs, it exports two char interfaces: $/dev/random$ and $/dev/urandom$. The quality of randomness is higher for reads from $/dev/random$ compared to that from $/dev/urandom$. When a user program reads from $/dev/random$, it gets strong (or true) random numbers, but reads from $/dev/urandom$ yield pseudo random numbers. The $/dev/random$ driver does not use formulae to generate strong random numbers. Instead, it gathers "environmental noise" (interval between interrupts, key clicks, and so on) for maintaining a reservoir of disorder (called an $entropy\ pool$) that seeds the random stream. To see the kernel's $input$ subsystem (discussed in Chapter 7) contributing to the entropy pool when it detects a keyboard press or mouse movement, look at $input\_event()$ defined in $drivers/input/input.c$:

```
void
input_event(struct input_dev *dev, unsigned int type,
unsigned int code, int value)
{
/* ... */
add_input_randomness(type, code, value); /* Contribute to entropy
pool */
/* ... */
}
```

To see how the core interrupt handling layer contributes inter-interrupt periods to the entropy pool, look at $handle\_IRQ\_event()$ defined in $kernel/irq/handle.c$:

```
irqreturn_t handle_IRQ_event(unsigned int irq,
struct irqaction *action)
{
/* ... */
if (status & IRQF_SAMPLE_RANDOM)
```