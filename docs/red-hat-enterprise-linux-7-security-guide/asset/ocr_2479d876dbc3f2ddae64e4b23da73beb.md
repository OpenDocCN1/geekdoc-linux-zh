command (note that all non-root users that need to communicate with the `pkcsslotd` daemon must be a part of the `pkcs11` system group):

```
`~]$ pkcsconf -t`
```

See the `pkcsconf(1)` manual page for a list of arguments available with the `pkcsconf` tool.

![](bbox=[0.08, 0.18, 0.2, 0.26])

> Keep in mind that only fully trusted users should be assigned membership in the `pkcs11` group, as all members of this group have the right to block other users of the `openCryptoki` service from accessing configured `PKCS#11` tokens. All members of this group can also execute arbitrary code with the privileges of any other users of `openCryptoki`.

# ### 4.9.4. Using Smart Cards to Supply Credentials to OpenSSH

The smart card is a lightweight hardware security module in a USB stick, MicroSD, or SmartCard form factor. It provides a remotely manageable secure key store. In Red Hat Enterprise Linux 7, OpenSSH supports authentication using smart cards.

To use your smart card with OpenSSH, store the public key from the card to the `~/.ssh/authorized_keys` file. Install the `PKCS#11` library provided by the `opensc` package on the client. `PKCS#11` is a Public-Key Cryptography Standard that defines an application programming interface (API) to cryptographic devices called tokens. Enter the following command as `root`:

```
`~]# yum install opensc`
```

# #### 4.9.4.1. Retrieving a Public Key from a Card

To list the keys on your card, use the `ssh-keygen` command. Specify the shared library (OpenSC in the following example) with the `-D` directive.

```
```text
~]$ ssh-keygen -D /usr/lib64/pkcs11/opensc-pkcs11.so
ssh-rsa AAAAB3NzaC1yc[...] +g4Mb9
```
```

# #### 4.9.4.2. Storing a Public Key on a Server

To enable authentication using a smart card on a remote server, transfer the public key to the remote server. Do it by copying the retrieved string (key) and pasting it to the remote shell, or by storing your key to a file (`smartcard.pub` in the following example) and using the `ssh-copy-id` command:

```
```text
~]$ ssh-copy-id -f -i smartcard.pub user@hostname
user@hostname's password:

Number of key(s) added: 1
```
```