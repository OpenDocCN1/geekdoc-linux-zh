The fields are:

+   1.  **login name**: as returned by getpwuid(getuid()) or tty name.
+   2.  **unused**: compat. with passwd.
+   3.  **Remote Address**: IP address of the calling host, either numeric or by name.
+   4.  **Local Address**: IP address of this machine, again numeric or by name.
+   5.  **Netmask**: in dotted decimal notation.
+   6.  **Comment field**: put whatever you want here.
+   7.  **protocol**: SLIP, CSLIP, etc.
+   8.  **MTU**: decimal number.

An example /etc/net/diphosts entry for a remote SLIP user might be:

```
Sfremd::145.71.34.1:145.71.34.2:255.255.255.0:SLIP wualt:SLIP,296
```

which specifies a SLIP link with remote address of 145.71.34.1 and MTU of 296, or:

```
Sfremd::145.71.34.1:145.71.34.2:255.255.255.0:CSLIP wualt:CSLIP,1006
```

which specifies a cSLIP-capable link with remote address 145.71.34.1 and MTU of 1006.

Therefore, all users who wish to be allowed a statically allocated dial-up IP access should have an entry in the /etc/diphosts. If you want users who call a particular port to have their details dynamically allocated, then you must have an entry for the tty device, and you must not configure a user-based entry. You should remember to configure at least one entry for each tty device that your dial-up users use, to ensure that a suitable configuration is available for them, regardless of which modem they call in on.

When a user logs in they will receive a normal login and password prompt, at which they should enter their SLIP-login user ID and password. If these verify ok, then the user will see no special messages and they should just change into SLIP mode at their end. The user should then be able to connect ok and be configured with the relevant parameters from the diphosts file.

![](bbox=[0.85, 0.56, 0.9, 0.7])