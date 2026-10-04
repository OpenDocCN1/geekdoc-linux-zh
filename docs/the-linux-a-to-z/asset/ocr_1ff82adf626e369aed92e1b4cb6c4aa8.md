+   - `/dev/ttyS0`
- `/dev/ttyS1`
- `/dev/ttyS2`
- `/dev/ttyS3`

As in the case of a modem, a common practice is to create a symbolic link to the serial device from /dev/mouse with a command like:

```
# ln -s /dev/ttyS1 /dev/mouse
```

# 9.3.2 Bus

If you are going out to buy a mouse, then unless you have a good reason to do otherwise, buy a serial mouse. If your computer already has a PS/2 mouse interface, or if you already have a bus mouse, or if you are determined that you want to buy a bus mouse anyway, then that is okay but the installation and configuration of these devices just takes more effort.

In general, a bus mouse will require its own interface card to be fitted inside your computer and the mouse itself will plug into that card. Sometimes a bus mouse interface will be fitted to some other card such as a video adaptor, so that the mouse will not take up an extra slot on your motherboard.

Having fitted the hardware to the machine, you will need to set the interface card up so that it generates an interrupt (IRQ) which does not conflict with any other hardware in your machine and then recompile the kernel to include the appropriate bus mouse support.

By default, most bus mouse interface cards use IRQ 5 as their interrupt number, but lots of other cards also use this as their default, so you will need to take some care over getting the choices right. The IRQ numbers you cannot use are:

```
0 1 2 6 8 13 14 and 15
```

as these are already in use for standard devices and cannot be changed. This leaves you with the choice of:

```
3 4 5 7 9 10 11 and 12
```

Of these, the first four are allocated for use by the standard serial and parallel ports, as follows:

| IRQ | Allocation |
|---|---|
| 3 | COM2 |
| 4 | COM1 |
| 5 | LPT2 |
| 7 | LPT1 |