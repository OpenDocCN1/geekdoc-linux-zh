The easiest way to dedicate a serial port for SLIP is the slattach program. This command is supported by most Linux versions. The slattach command takes the device name of the serial port as an argument. For example, to dedicate the second serial port (\texttt{/dev/cua1} or \texttt{/dev/tty2A}, depending on the operating system) to SLIP, issue the following command or a similar command with the proper device name instead of \texttt{/dev/cua1} (which is the Linux convention for modem serial ports):

```
slattach /dev/cua1 &
```

The slattach command is sent into background mode by the ampersand. Failure to send to background means the terminal or the console the command is issued from is not usable until the process is terminated. You can embed the slattach command in a start-up file such as the rc files or a session shell startup file if you want.

Once the slattach command has executed successfully, the serial port is set to the first SLIP device (usually \texttt{/dev/sl0}). If you are using more than one serial port for SLIP lines, you need to issue the command for each line. By default, most Linux systems set the SLIP port to use CSLIP (compressed SLIP). If you want to override this action, use the -p option and this device name:

```
slattach -p slip /dev/cua1 &
```

It's important to make sure that both ends of the connection use the same form of SLIP. There is slip6 (a 6-bit version of SLIP) and adaptive SLIP (which adjusts to whatever is at the other end of the connection). For example, you cannot set your device for CSLIP and communicate with another machine running 6-bit SLIP.

After the serial port is set for SLIP usage, configure the network interface using the same procedure as normal network connections. For Linux, the commands used are ifconfig and route. For example, if your machine is called merlin and you are calling the remote machine arthur, issue the following commands:

```
ifconfig sl0 merlin-slip pointopoint arthur
route add arthur
```

The ifconfig command above configures the interface merlin-slip (the local address of the SLIP interface) to be a point-to-point connection to arthur. The route command adds the remote machine called arthur to the routing tables.

If you want to use the SLIP port for access to the Internet, it must have an IP address and an entry in the /etc/hosts file. That gives the SLIP system a valid entry on the Internet.

After the ifconfig and route commands execute, you can test and use your SLIP net- work. If you decide to remove the SLIP interface in the future, you must first remove the