# General Troubleshooting Techniques 607

+   - Be patient and methodical. You're unlikely to find solutions in the last few hours of a 12-hour troubleshooting session. You can probably no longer look at the problem methodically after so long. Rest your brain and your eyes, and then try again. Don't forget to eat and sleep!

+   - If something worked yesterday but suddenly doesn't work today, it is probably not a configuration problem. Again, look at /var/log/messages to see if there is a message that will point to the problem. Check anything that has changed since the last time it worked to determine whether something changed caused the error. If you still don't find it (and you know no one has changed the configuration from the working one), don't spend a lot of time reworking configuration files; consider hardware.

+   - Remember that many services have a debugging switch that allows you to pass in parameters and/or increases the number of messages that the service logs to /var/log/messages. Also use the verbose switch wherever it exists to ensure that you receive the most information possible about what the service is doing. Some services have syntax checkers (for example, tcpchk for networking) to determine whether the configuration files have errors. tcp has a great utility called tcpmatch, which allows you to see whether your system would accept connections from a hostname that you pass as a parameter.

+   - Remember many services depend on the ability to look up an IP address from a hostname with nslookup or even look up a hostname in reverse with nslookup (reverse lookup).

Login programs are often due to an error in the related PAM file:

```
login      /etc/pam.d/login
rlogin    /etc/pam.d/rlogin
KDM       /etc/pam.d/kdm
GDM       /etc/pam.d/gdm
XDM       /etc/pam.d/xdm
SSH       /etc/pam.d/sshd
```

+   - When specifying a library path, ensure that you've spelled everything correctly and that the case is correct.

+   - The compiler never lies, although it can obfuscate. If you have an error message that you don't understand, there is a problem in the code. The compiler may interpret the true source of the problem as being OK, though, and report an error on some lines later, when the compiler's interpretation finally breaks down. Compiler messages are also just plain cryptic. Look to determine what the error means. To confuse the issue a bit, bad hardware sometimes cause the compiler to give you an error that might send you down the wrong path.

![](bbox=[0.913, 0.633, 0.993, 0.853])