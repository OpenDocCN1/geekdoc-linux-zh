# # Setting the Modem

Whether your data communications use terminal emulation or connect to a network through a phone line, you'll need to have your modem set up properly. set up the `setup` program in Slackware can do the job. To run the `setup` program, type `setup` at the prompt:

```
# setup
```

![](bbox=[0.08, 0.26, 0.84, 0.34])

Next, you'll see a familiar installation screen that presents you with menu choices. Select the Configure option to set up your modem and mouse. (You can also build a boot disk this way, but we'll skip the boot-disk options for now.) When the next window asks whether you'd like to set up your modem; select Yes.

You'll have only one step once you get to your modem choice. You'll need to pick which serial port the modem is connected to. Because mine is connected to COM1, I need to select cua0. The cua is for the modem communication port, and the number following (in this case, zero) represents which of the four COM ports the modem is using. (Because Linux is written in C, it counts the same way C programs do: it starts with zero instead of one.) Figure 1-6 shows the modem selection screen, which includes the serial ports.

![](bbox=[0.08, 0.62, 0.64, 0.8])

When you've set up the modem, you can go on to the mouse setup. But take a look at the file type for /dev/modem. You'll see a symbolic link that indicates the actual serial port to which your modem is connected. Here's an example:

```
tigerden:/home/stripes$ ls -l /dev/modem
lrwxrwxrwx  1 root  root  4 Aug  3 23:39 /dev/modem -> cua0
```