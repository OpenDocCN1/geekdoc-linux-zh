# Connecting to serial consoles

The basic steps for connecting to a serial console are as follows:

+   - Attach a cable between the serial port on your UNIX system and the device you want to talk to. See the discussion earlier in this chapter about the various connector types and pinouts that might be necessary. You will most likely need a null modem cable. These are available at your nearest computer store.

+   - Install or identify the terminal communication software you will use on your UNIX or Linux system. Decades ago, the standard command for this was cu or tip. You can still use these in a pinch, but modern-day alternatives such as minicom and picocom are. Linux distributions normally include one of these; on other systems, you may need to install the software yourself (freshmeat.net/projects/minicom or freshmeat.net/projects/picocom, respectively).

+   - Configure your communication software to open the correct device file (see the discussion earlier in this chapter). Usually, names like /dev/ttya, /dev/tty1, /dev/ttyS0, or /dev/S0 are good first guesses.

+   - Set the baud rate, stop bits, and flow control to match the defaults used on the target device. These parameters are usually outlined in the manual for device, but you can also try possible combinations. If you don't know the correct baud rate, an "old dog" trick is to connect and type a few characters. If you have to type multiple characters to get a single character of garbage, you've set the baud rate too high. If typing one or two characters produces many characters of garbage, you've set the baud rate low. Shhhh... don't tell anyone!

+   - Once you've successfully connected, you should be able to enter commands on the remote console. If you find that the device suddenly hangs on long output, you have probably misconfigured the flow control; typing <Control-Q> will sometimes get you by.

If you have trouble connecting, the first debugging step should be to remove the crossover in the cable, or to add one if you didn't start with one. Don't forget that you're connecting to a remote UNIX box, you'll need to set up a getty to listen for your connection and present a login prompt.

Exercises begin on the next page.