> **NOTE**
> If you are using the default Apache install, you can also use a name-based virtual hosting method rather than burning an IP address for each virtual domain. Consult the Apache home page, http://www.apache.org/, for more information regarding name-based IP addressing. This type of IP addressing normally requires a couple of additional lines in your httpd.conf file, the default configuration file for setting up the web server.

# # Using the Hardware Device Files

Another method of checking your devices and verifying that the hardware por-tion of the setup is working well is to look in the /proc/ directory. This directory does not contain the static files that are usually found in most Linux directories. These are files that are generated spontaneously to reflect the state of the kernel. Because this directory monitors systems files that are in a state of constant flux, they cannot be rewritten or cleared constantly. It is better to generate their con-tent on the fly.

One of the best methods for checking the IRQ of a network device or monitor-ing the input/output ports of different devices is to use the cat command and output the results to the console.

![](bbox=[0.5, 0.6, 0.55, 0.63])

If you wanted to see what IRQs were in use by the different devices, you would enter the following command:

```bash
# cat /proc/interrupts
```

To check the IO ports in use, use this command:

```bash
# cat /proc/ioports
```

You use the same format to check the current state of memory use:

```bash
# cat /proc/meminfo
```

This directory contains additional information about your system, and you can output each file to the console and examine the results.
This is useful if you are installing a new network card that has a conflict with another device. Such a conflict can happen between