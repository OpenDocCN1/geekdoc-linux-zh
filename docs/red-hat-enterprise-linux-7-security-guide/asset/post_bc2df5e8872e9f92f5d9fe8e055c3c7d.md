
Based on the above syntax, a command for generating an encrypted key using the already created trusted key can be constructed as follows:

```sh
~]$ keyctl add encrypted enckey "new trusted:kmk 32" @u
159771175
```

To create an encrypted key on systems where a TPM is not available, use a random sequence of numbers to generate a user key, which is then used to seal the actual encrypted keys.

```sh
~]$ keyctl add user krmk-user "`dd if=/dev/urandom bs=1 count=32 2>/dev/null`" @u
427069434
```

Then generate the encrypted key using the random-number user key:

```sh
~]$ keyctl add encrypted enckey "new user:krmk 32" @u
1012412758
```

The `list` subcommand can be used to list all keys in the specified kernel keyring:

```sh
~]$ keyctl list @u
2 keys in keyring:
427069434: --alswrv 1000 1000 user: krmk-user
1012412758: --alswrv 1000 1000 encrypted: enckey
```

> **IMPORTANT**
> 
> Keep in mind that encrypted keys that are not sealed by a master trusted key are only as secure as the user master key (random-number key) used to encrypt them. Therefore, the master user key should be loaded as securely as possible and preferably early during the boot process.

## 4.9.5.2. Additional Resources

The following offline and online resources can be used to acquire additional information pertaining to the use of trusted and encrypted keys.

### Installed Documentation

- `keyctl(1)` – Describes the use of the `keyctl` utility and its subcommands.

### Online Documentation

- [Red Hat Enterprise Linux 7 SELinux User's and Administrator's Guide](#) – The *SELinux User's and Administrator's Guide* for Red Hat Enterprise Linux 7 describes the basic principles of SELinux and documents in detail how to configure and use SELinux with various services, such as the Apache HTTP Server.
- [https://www.kernel.org/doc/Documentation/security/keys-trusted-encrypted.txt](#) – The official documentation about the trusted and encrypted keys feature of the Linux kernel.

### See Also

- Section A.1.1, “Advanced Encryption Standard – AES” provides a concise description of the Advanced Encryption Standard.
- Section A.2, “Public-key Encryption” describes the public-key cryptographic approach and the various cryptographic protocols it uses.

## 4.9.6. Using the Random Number Generator

In order to be able to generate secure cryptographic keys that cannot be easily broken, a source of random numbers is required. Generally, the more random the numbers are, the better the chance of obtaining unique keys. Entropy for generating random numbers is usually obtained from computing environmental “noise” or using a hardware random number generator.

The `rngd` daemon, which is a part of the `rng-tools` package, is capable of using both environmental noise and hardware random number generators for extracting entropy. The daemon checks whether the data supplied by the source of randomness is sufficiently random and then stores it in the random-number entropy pool of the kernel. The random numbers it generates are made available through the `/dev/random` and `/dev/urandom` character devices.

The difference between `/dev/random` and `/dev/urandom` is that the former is a blocking device, which means it stops supplying numbers when it determines that the amount of entropy is insufficient for generating a properly random output. Conversely, `/dev/urandom` is a non-blocking source, which reuses the entropy pool of the kernel and is thus able to provide an unlimited supply of pseudo-random numbers, albeit with less entropy. As such, `/dev/urandom` should not be used for creating long-term cryptographic keys.

To install the `rng-tools` package, issue the following command as the root user:

```sh
[~]# yum install rng-tools
```

To start the `rngd` daemon, execute the following command as root:

```sh
[~]# systemctl start rngd
```

To query the status of the daemon, use the following command:

```sh
[~]# systemctl status rngd
```

To start the `rngd` daemon with optional parameters, execute it directly. For example, to specify an alternative source of random-number input (other than `/dev/hwrandom`), use the following command:

```sh
[~]# rngd --rng-device=/dev/hwrng
```

The above command starts the `rngd` daemon with `/dev/hwrng` as the device from which random numbers are read. Similarly, you can use the `-o` (or `--random-device`) option to choose the kernel device for random-number output (other than the default `/dev/random`). See the `rngd(8)` manual page for a list of all available options.

To check which sources of entropy are available in a given system, execute the following command as root:

```sh
[~]# rngd -vf
Unable to open file: /dev/tpm0
```

Available entropy sources:
DRNG

### NOTE

After entering the `rngd -v` command, the according process continues running in background. The `-b, --background` option (become a daemon) is applied by default.

If there is not any TPM device present, you will see only the Intel Digital Random Number Generator (DRNG) as a source of entropy. To check if your CPU supports the RDRAND processor instruction, enter the following command:

```sh
$ cat /proc/cpuinfo | grep rdrand
```

### NOTE

For more information and software code examples, see Intel Digital Random Number Generator (DRNG) Software Implementation Guide.

The `rng-tools` package also contains the `rngtest` utility, which can be used to check the randomness of data. To test the level of randomness of the output of `/dev/random`, use the `rngtest` tool as follows:

```sh
$ cat /dev/random | rngtest -c 1000
rngtest 5
Copyright (c) 2004 by Henrique de Moraes Holschuh
This is free software; see the source for copying conditions. There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR
PURPOSE.

rngtest: starting FIPS tests...
rngtest: bits received from input: 20000032
rngtest: FIPS 140-2 successes: 998
rngtest: FIPS 140-2 failures: 2
rngtest: FIPS 140-2(2001-10-10) Monobit: 0
rngtest: FIPS 140-2(2001-10-10) Poker: 0
rngtest: FIPS 140-2(2001-10-10) Runs: 0
rngtest: FIPS 140-2(2001-10-10) Long run: 2
rngtest: FIPS 140-2(2001-10-10) Continuous run: 0
rngtest: input channel speed: (min=1.171; avg=8.453; max=11.374)Mibits/s
rngtest: FIPS tests speed: (min=15.545; avg=143.126; max=157.632)Mibits/s
rngtest: Program run time: 2390520 microseconds
```

A high number of failures shown in the output of the `rngtest` tool indicates that the randomness of the tested data is insufficient and should not be relied upon. See the `rngtest(1)` manual page for a list of options available for the `rngtest` utility.

Red Hat Enterprise Linux 7 introduced the `virtio RNG` (Random Number Generator) device that provides KVM virtual machines with access to entropy from the host machine. With the recommended setup, `hw rng` feeds into the entropy pool of the host Linux kernel (through `/dev/random`), and QEMU will use `/dev/random` as the source for entropy requested by guests.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_119_0.png)

**Figure 4.1. The virtio RNG device**

Previously, Red Hat Enterprise Linux 7.0 and Red Hat Enterprise Linux 6 guests could make use of the entropy from hosts through the `rngd` user space daemon. Setting up the daemon was a manual step for each Red Hat Enterprise Linux installation. With Red Hat Enterprise Linux 7.1, the manual step has been eliminated, making the entire process seamless and automatic. The use of `rngd` is now not required and the guest kernel itself fetches entropy from the host when the available entropy falls below a specific threshold. The guest kernel is then in a position to make random numbers available to applications as soon as they request them.

The Red Hat Enterprise Linux installer, **Anaconda**, now provides the **virtio-rng** module in its installer image, making available host entropy during the Red Hat Enterprise Linux installation.

## 4.10. USING NETWORK-BOUND DISK ENCRYPTION

The Network-Bound Disk Encryption (NBDE) allows the user to encrypt root volumes of hard drives on physical and virtual machines without requiring to manually enter a password when systems are restarted.

In Red Hat Enterprise Linux 7, NBDE is implemented through the following components and technologies:
