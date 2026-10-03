
Now that we have a key, we can use it to sign a kernel module.

To sign a module, use the sign script, which is a simple shell script:

```
#!/bin/bash
module=$1
key=$2

# strip out only the sections that we care about
./mod $module $module.out

# sha1 the sections
sha1sum $module.out | awk "{print \$1}" > \
$module.sha1

# encrypt the sections
gpg --no-greeting -e -o - -r $key $module.sha1 > \
$module.crypt

# add the encrypted data to the module
objcopy --add-section module_sig=$module.crypt \
$module

# remove the temporary files
rm $module.out $module.sha1 $module.crypt
```

The first thing the script does is run the program mod on the kernel module. This program strips out only the sections that we care about in the ELF file and outputs them to a temporary file. The mod program is described in more detail later.

After we have an ELF file that contains only the sections we want, we generate a SHA1 hash of the file using the sha1sum program. This SHA1 hash then is encrypted using GPG, the key is passed to it and this encrypted file is written out to a temporary file. The encrypted file is added to the original module as a new ELF section with the name module-sig. This is done with the program objcopy. And that is it. Using common programs already present on a Linux machine, it is easy to create a SHA1 hash, encrypt it and add it to an ELF file.

The mod program also is quite simple. It takes advantage of the fact that the libbfd library knows how to handle ELF files and manipulates them in different ways; it is based on the binutils program objdump. Because the libbfd library handles all of the heavy ELF logic, the mod program simply can iterate through all the sections of the ELF file it wants to with the following code:

```
for (section = abfd->sections;
    section != NULL;
    section = section->next) {
    if (section->flags & SEC_HAS_CONTENTS) {
        if (bfd_section_size(abfd, section) == 0)
            continue;

        /* we only care about sections with "text"
           or "data" in their names */
        name = section->name;

```

```
if ((strstr(name, "text") == NULL) &&
    (strstr(name, "data") == NULL))
    continue;

size = bfd_section_size(abfd, section);
data = (bfd_byte *)malloc(size);

bfd_get_section_contents(abfd, section,
                    (PTR)data,
                    0, size);

stop_offset = size / opb;

for (addr_offset = 0;
    addr_offset < stop_offset;
    ++addr_offset) {
    fprintf(out, "%c", data[addr_offset]);
}
    free(data);
}
}
```

Now that we can sign a kernel module and the kernel knows how to detect this signature, the only remaining piece is to put our public key into the kernel so it can decrypt the signature successfully. A lot of discussion on the linux-kernel mailing list recently has centered on how to handle keys within the kernel properly. That discussion has produced some good proposals for how this aspect will be handled in the 2.7 kernel series. But for now, we do not worry about properly handling keys in flexible ways, so we compile it in directly.

First we need to get a copy of our public key. To do this, tell GPG to extract the key to a file called public_key:

```
$ gpg --export -o public_key
```

To help manipulate GPG public keys, some developers at Ericsson created a simple program called extract_pkey to help dissect the keys into their different pieces. I have modified that program to generate C code for the public key.

Run the extract_pkey program and point it at the public_key file you generated previously. Have it send the output to a file called rsa_key.c:

```
$ extract_pkey public_key > rsa_key.c
```

After this step is finished, move that rsa_key.c on top of the file in the security/rsa/ directory, replacing my public key with yours:

```
$ mv rsa_key.c ~/linux/linux-2.6/security/rsa/
```

Now you have generated a public and private RSA key pair and placed your public key into the kernel directory. Build the patched kernel, making sure to select the Module signature checking option, and then install it. If you boot in to this kernel, you will be allowed to load only the modules you have signed with your key, so be careful and test this only on a development machine.

## What Is Left to Do?

As shown in this article, a number of different steps are required to generate a key, sign a kernel module and place the public key into the kernel image. This still is a rough development project. In order to make it more acceptable to the kernel developers and to the Linux community in general, these steps need to be automated, making it easier to sign all kernel modules and handle the public key.

Besides the obvious need to simplify the use of this feature, some other future goals of this project include:

- Move the RSA code into the generic crypto framework, allowing other kernel features to use it.
- Allow more than one public key to be present in the kernel, letting multiple sources of signed kernel modules run in a single machine.
- Simplify the signing logic to allow GPG’s native signing functionality or possibly the functionality provided in the bsign program to be used, instead of the custom mod program.

## Acknowledgements

I would like to thank the developers at Ericsson, who have created a kernel patch and program called digsig, for allowing me to use their port of GPG to the kernel. I previously had done this, but the implementation was horrible; thankfully, they released their port and were very helpful. The digsig kernel patch allows users to sign programs and prevents the kernel from running any program not signed. More information about this project can be found at sourceforge.net/projects/digsig.

I also would like to thank my employer, IBM, for allowing me to work on this project, and Don Marti, for prodding me to finish it and write this article.

Greg Kroah-Hartman currently is the Linux kernel maintainer for a variety of different driver subsystems. He works for IBM, doing Linux kernel-related things, and can be reached at greg@kroah.com.

![](img/3e9d313887e2c1cabeb5043769cbf08f_54_0.png)

## Cacti: www.raxnet.net/products/cacti

![](img/3e9d313887e2c1cabeb5043769cbf08f_54_1.png)

Cacti is similar in some ways to MRTG but is easier to set up and administer and, by default, graphs more than traffic. But, some Cacti users haven’t stopped there; they’ve graphed Web server hits, bind statistics, weather and more. A

quick look at the Cacti home page is a real eye-opener. I’m sure you could use it to graph even more with a few quick scripts. Requires: rrdtool, MySQL, Web server, PHP with SNMP and MySQL support, snmpd, Perl and a graphical Web browser.

> — DAVID A. BANDEL

## www.asacomputers.com

### Hardware Systems for the Open Source Community—since 1989
[ Linux, FreeBSD, NetBSD, OpenBSD, Solaris... ]

![](img/3e9d313887e2c1cabeb5043769cbf08f_54_2.png)

### 4TB in 4U—$8,299

Intel E7501, 2 x Intel Xeon 2.4GHz
1 GB ECC DDR Max: 16GB
1 x 10/100 LAN
1 Gigabit LAN
Raid 0,1,5,etc.
CD, Floppy
Redundant Hot-Swap Power Supply

### 2U Dual Xeon SCSI—$2,260

6 Front-removable Hot-Swap SCSI bays
2 x Intel Xeon 2.4 GHz Max: 2
1 GB ECC DDR Max: 16GB
1 x 36GB U320 SCSI Drives
Raid optional Max: 876GB Storage
CD, Floppy
Dual Gig ports
1 Extra 5.25 Drive Bay
Hot-plug redundant power supply

### Dual AMD Opteron in 1U—$1,729

2 x AMD Opteron 240
1 GB DDR ECC Registered Memory
1 x 40 GB IDE
Gigabit LAN

![](img/3e9d313887e2c1cabeb5043769cbf08f_54_3.png)

### Space-saving Mini-1U Dual Xeon IDE—$1,529

![](img/3e9d313887e2c1cabeb5043769cbf08f_54_4.png)

1U 14" Depth
533 MHz FSB
2 x Intel Xeon 2.4 GHz
1 GB DDR ECC Memory
40 GB IDE HDD
1 GIG, 1 10/100 LAN

### 1U P4 Entry-level Server—$735

1 x Intel P4 2.4 GHz
256 MB DDR ECC Memory
40 GB IDE Drive
CD, 2 x 10/100 LAN

### 1U Dual Xeon SCSI—$1,558

SuperMicro 6013P-8 Barebones
Dual Intel Xeon 2.4 GHz 533 FSB
512 MB DDR ECC Max: 12GB
36 GB 10K rpm SCSI
3 Hot-Swap SCSI Drive Bays
CD, Floppy
Dual Gig, VGA onboard
Raid optional

### ASA Colocation

$50 per month for
1U Rack - 20 GB/month

### ASA Colocation Special

First month of colocation free.*

### Storage Solutions

IDE, SCSI, Fiber RAID solutions
TB storage options
3Ware, Promise, Adaptec,
ICP-Vortex, LSI, CMD, Chaparral,
Mylex controllers
JMR, Kingston/Storcase solutions

### Clusters

Rackmount and Desktop nodes
HP, Intel, 3Com, Cisco switches
KVM or Cyclades Terminal Server
APC or Generic racks

All systems installed and tested with user’s choice of Linux distribution [free]. ASA Colocation—$50 per month

## ASA Computers, Inc.
1-800-REAL-PCS

2354 Calle Del Mundo, Santa Clara, CA 95054
TEL: (408) 654-2900 • FAX: (408) 654-2910
E-MAIL: sales@asacomputers.com
Free delivery in Silicon Valley*
Open on Sat. too—10 to 1

![](img/3e9d313887e2c1cabeb5043769cbf08f_54_5.png)

## www.asacomputers.com
www.b2bforsale.com
