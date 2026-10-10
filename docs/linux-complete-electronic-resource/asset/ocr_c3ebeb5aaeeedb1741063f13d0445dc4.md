This gives the kernel version and the date on which this kernel was compiled-which should give you a pretty good idea of what is going on.

# Did You Compile PPP Kernel Support as a Module?

If you compiled your kernel PPP support as a module, but did not make and install the modules, then you can get this error. Check the kernel-HOWTO and the README file in /usr/src/linux.

Another module-connected possibility is that you are expecting required modules to be automatically loaded, but are not running the kernel daemon (which auto-loads and unloads modules on the fly). Check the kernel mini-HOWTO for information on setting up kernel.

# Are You Using the Correct Version of PPP for Your Kernel?

You must use ppp-2.2 with kernel version 2.0.x. You can use ppp-2.2 with kernel version 1.2.x (if you patch the kernel); otherwise you must use ppp-2.1.2.

# Are You Running pppd as Root?

If you are not running pppd as the root user (and pppd is not suid to root), you can receive this message.

# My Modem Connects but PPP Never Starts Up

There are innumerable variations on this (take a look in comp.os.linux.) .

A very common mistake is that you have mistyped something in your scripts. The only thing to do here is to make sure you are logging the chat conversation between your Linux box and the server into your syslog (/var/log/messages) and then go through this line by line. You may need to dial into the PPP server manually to check things out again.

You need to check the log against the actual prompts very carefully-and bear in mind that we humans have a tendency to read what we think we have typed-not what is actually there.

# The syslog Says Serial Line Is Not 8 Bit Clean...

There are variations on this too-such as serial line looped back, etc., and the cause can be one (or a sequence) of a number of things.

![](bbox=[0.92, 0.52, 0.98, 0.65])