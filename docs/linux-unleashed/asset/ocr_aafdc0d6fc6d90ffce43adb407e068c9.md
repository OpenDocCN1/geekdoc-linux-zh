Upon receipt of an interrupt, the operating system suspends whatever it is executing and processes the interrupt. In most cases, interrupts are handled by the device driver. Interrupts must be checked to ensure that they are valid and do not affect operation of a process underway, except to suspend it momentarily.

A problem with handling interrupts is that the interrupt should not suspend the Linux kernel's operation or that of the device drivers themselves, except under controlled conditions. Interrupts that are not properly handled or carefully checked can cause suspension of a device driver that was processing the I/O that the interrupt requested.

The processing of an interrupt is usually suspended during the stages when critical operation would be affected. The areas of device driver code that should not allow an interrupt to stop their processing are termed *non-stoppable* or *critical* code. Typically, interrupt suspension during critical code segments is performed by raising the CPU priority to or greater than the interrupt priority level. After critical code execution, the CPU priority level is lowered again.

Interrupt priority is usually manipulated with four functions: `sp15()`, `sp16()`, `sp17()`, and `splx()`. Calling one of the first three causes interrupts *not* to be acknowledged during processing. `sp15()` disables disk drives, printer, and keyboard interrupts. `sp16()` disables the system clock, while `sp17()` disables all interrupts, including serial devices. These three functions always return a code indicating the previous value of the interrupt level. `splx()` is used to restore interrupts to their previous values.

Therefore, before processing critical code, embedding the command

```
old_level = sp15();

```

in the device driver source disables interrupts until the following command is issued:

```
splx(old_level);

```

Multiple level changes are combined into device drivers as in the following example:

```
int level_a, level_b;
level_a = sp15();
/* do any code that can't be */
/* interrupted by disk drives */
level_b = sp17();;
/* do all code that can't be */
/* interrupted by anything   */
splx(level_b);
/* any final code that's not */
/* interrupted by disk drives */
splx(level_a);

```