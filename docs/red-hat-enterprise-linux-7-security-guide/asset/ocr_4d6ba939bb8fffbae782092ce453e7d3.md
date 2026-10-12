Prior to any operations with keys, relevant kernel modules need to be loaded. For trusted keys, it is the `trusted` module, and for encrypted keys, it is the `encrypted-keys` module. Use the following command as the `root` user to load both of these modules at once:

```
~~~bash
~]# modprobe trusted encrypted-keys
~~~
```

Trusted and encrypted keys can be created, loaded, exported, and updated using the `keyctl` utility. For detailed information about using `keyctl`, see keyctl(1).

# **NOTE**

In order to use a TPM (such as for creating and sealing trusted keys), it needs to be enabled and active. This can be usually achieved through a setting in the machine’s BIOS or using the `tpm_setactive` command from the `tpm-tools` package of utilities. Also, the `TrouSers` application needs to be installed (the `trousers` package), and the `tcsd` daemon, which is a part of the `TrouSers` suite, running to communicate with the TPM.

To create a trusted key using a TPM, execute the `keyctl` command with the following syntax:

```
~~~bash
keyctl add trusted name "new keyLength [options]" keyring
~~~
```

Using the above syntax, an example command can be constructed as follows:

```
~~~bash
~]$ keyctl add trusted kmk "new 32" @u
642500861
~~~
```

The above example creates a trusted key called `kmk` with the length of 32 bytes (256 bits) and places it in the user keyring (@u). The keys may have a length of 32 to 128 bytes (256 to 1024 bits). Use the `show` subcommand to list the current structure of the kernel keyrings:

```
~~~bash
~]$ keyctl show
Session  Keyring
    -3 --alswrv     500   500  keyring: _ses
97833714 --alswrv   500    -1 \_ keyring: _uid.1000
642500861 --alswrv  500   500  \_  trusted: kmk
~~~
```

The `print` subcommand outputs the encrypted key to the standard output. To export the key to a user-space blob, use the `pipe` subcommand as follows:

```
~~~bash
~]$ keyctl pipe 642500861 > kmk.blob
~~~
```

To load the trusted key from the user-space blob, use the `add` command again with the blob as an argument:

```
~~~bash
~]$ keyctl add trusted kmk \`load \`cat kmk.blob\`\` @u
268728824
~~~
```

The TPM-sealed trusted key can then be employed to create secure encrypted keys. The following command syntax is used for generating encrypted keys:

```
~~~bash
~]$ keyctl add encrypted name "new [format] key-type:master-key-name
keyLength" keyring
~~~
```