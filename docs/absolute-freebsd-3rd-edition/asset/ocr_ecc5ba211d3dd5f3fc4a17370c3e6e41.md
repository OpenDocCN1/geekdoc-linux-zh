simultaneous new connections; you’ll probably have to tune your app well before you hit this point.

# ## Polling

Some gigabit cards can improve their performance with *polling*. Polling takes the time-honored idea of interrupts and IRQs and boots it out the window, replacing it with regular checks for network activity. In the classic interrupt-driven model, whenever a packet arrives at the network card, the card demands attention from the CPU by generating an interrupt. The CPU stops whatever it’s doing and handles that data. This is grand, and even desirable, when the card doesn’t process a huge amount of traffic. Once a system starts handling large amounts of data, however, the card generates interrupts continuously. Instead of constantly interrupting, the system is more efficient if the kernel grabs network data from the card at regular intervals. This regular checking is called *polling*. Generally speaking, polling is useful only if you push large amounts of traffic.

Polling isn’t available as a kernel module as of this writing, since it requires modifications to device drivers. This also means that not all network cards support polling, so be sure to check polling(4) for the complete list. Enable polling by adding DEVICE_POLLING to your kernel configuration. After your reboot, enable polling on a per-interface basis with ifconfig(8).

```
```
# ifconfig em0 polling
```
```

Similarly, disable polling with the argument -nopolling. The ifconfig(8) command also displays if polling is enabled on an interface. As you can enable and disable polling on the fly, enable polling when your system is under a heavy load and see whether performance improves.

Polling is used only on older cards. 10GB cards and faster can’t poll.

# ### Other Optimizations