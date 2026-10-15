# Login via the Modem

The dial-up connections are protected in a similar manner to the network connections. The getty program manages logins through a serial line or modem. It listens for the modem carrier signal and launches a login program when a connection is attempted. For the modem logins, we modified the getty program (a code fragment is in Listing 13.4) to launch our login wrapper program instead of the standard login program. If the challenge is correctly answered, the user is presented with a normal login prompt. If the challenge is incorrectly answered, getty exits immediately and the connection is severed.

# Listing 13.3 An example /etc/keyfile, which stores a user's SNK user ID.

```
# This file contains the encryption keys that have been
# installed in the SecureNet key which users use to log
# into the system from remote sites.
# The format of the file is as follows:
#    userid val_1 ... val_8 checksum
#
# where: userid - is the name of the user that's
#        entered at the SNK login prompt.
#
#        val_1 to val_8 - are the 8 octal values that have
#        been entered into the SecureNet key.
#
#        checksum - is the checksum value provided by the
#        SecureNet key.
#
# Author: Mark Dapoz, Bergen Scientific Centre
#
# SNK key number 1
#    Owner: Mark Dapoz
md 115 136 014 154 147 060 136 042 0908a5
#
# SNK key number 2
#    Owner: Rob MacKinnon
robmack 001 156 155 167 077 172 024 133 a860d0
```