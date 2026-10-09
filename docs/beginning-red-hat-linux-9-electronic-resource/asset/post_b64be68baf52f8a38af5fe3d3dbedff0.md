
## Chapter 4

This produces the following response – quite detailed isn't it? Most importantly it reveals the vendor's name and signing date, which is handy if you've got a key on your system, but aren't sure who it's from, or if it is still in date:

| Field | Value | Field | Value |
| :--- | :--- | :--- | :--- |
| Name | gpg-pubkey | Relocations | (not relocatable) |
| Version | db42a60e | Vendor | (none) |
| Release | 37ea5438 | Build Date | Sun 20 Apr 2003 14:10:53 BST |
| Install Date | Sun 20 Apr 2003 14:10:53 BST | Build Host | localhost |
| Group | Public Keys | Source RPM | (none) |
| Size | 0 | License | pubkey |
| Signature | (none) | | |

Summary: gpg(Red Hat, Inc <security@redhat.com>)
Description:
-----BEGIN PGP PUBLIC KEY BLOCK----
Version: rpm-4.1 (beecrypt-2.2.0):

mQGiBDFqVd9gRBADBKr3Bl6PO8BQOHoSJoD6p9U7Yv17pjTZqioviPwXFc+DCW4du8HQZcxzA5
7m88sAlLlKiF9x9coJuHDZm130+p5Bgn9mWSWHLaB3R31KXdpQXYccovTMQgx6wvYRG15Psw8QyD
LhjVfUF51X14Xt6bpPbWUB6vY2KZ5Z37pB1UUOiMrx3wCgobNVYEDGawYJucc5z5ZB1oF/41G8kE
AKii6q7Gu/vhXxNLS6mi5oNnPvybyngiw/23dKjSZGV7rKANEK2mxgi1VB+vc/uC4k49XJJ
fCZg1igusPFV3G5a+Y/7jsiLktQvcIILPncoTdiV+ENmHRsBdidP9DzKBVbgWnSDnqG6KrZ7
T6AL274VMpjGxxxWU6vV2xSWXCLPA/9P/vt1mA8CZNjxggT-K5GGTLDNJ/cmHuvu5VnFmwFg4b
/VGo2Jr8mhLUgo1EbE6zeGMaZbUcpDco8D5fiQmfTs+ ++pC6pRJLJKzKe1/32N2w4qzPcR
MCiBURxESPjCLd4Y5+rpO8E4K4OHC/4BuHN931iCScPlOcrWsQZ7UdqfQ5LQlUmVkIEhhdCwg
SW5jIDxzdXNlcm1lOeUBvZW8RYXQYxY29+PoHVBMRaGAvaBQJ361Q4AwsKAwMLvAWpDIGBAh
AAOJCEGRGm3b0gqvOesBQAnRVTg7BZ5HmllPHCap8FPedKdKi2AJ9ao8BSxLDmPOEF175mpTr
KYHFPr6cRDQQ361RlyEagAokgjX2Jb+3bZsk8JrAR0RIXBHD05UlMh27qFzLbT6npXwXYIotVn
OKZ/+1MDj+oEBlA2au40dddYalWp06v3d+Xy50t+5ab22fiQ2dh7wCwqxRkzR+/H5TlbmG+
hv+TdY1fqIXOWEfOXMtWWGSSVwyUsmN3yj3L01a8+QqSCstCauD20FoIGHwnb/glHu1NmNE
S6uDUqjFBE6EANgQhPcoOoIhHJ2oIO8ujQjt+vNarU8Hj/8/izqv5e7MxOGvSJKe/WX3StB
B/t/WYutpyl2wh1JJsFDblLv/t8Co2tXpJgx5mVA3RK3l+/Ta+On+1iEUuLoB+1lfft7GV/0cAc
waZDBQyrE4SKQRWamBS8KX0lOmYGmpXvPhYHInbDMLOkrwMTNnqSFRooJJRhexDxWmpTWK
ti/PRr9L2J1lP2ed0Xyzm8+v3gLYouliSba+8GLy+ p1T2QoSOGasVfZ7AQ80XbWJyRymX
Qp+8DeTeOTELKOL2/itDOpGHM07SsVVOR6cmX4ViRrcWB5KejaNVdrE54XfDOD4NmGwi63u
QcZ4zRka+kwEZtmbz3tHSRCRCE+Y7YYYpE1f/6wYPqQFiYFUwlfqAi6f6Lb1JhYWh8v0Gvj
8KmcwWKK4jg8klbXgj4/TzQSX77uYkqmi1eqweK2OzeOatcubsNNQoulCwmi1JghGBBgRAG
bQI36lRYaAAOJECGRGm3bQgQYoYhYAjn7hVDY/FUAGgmtZpwVp91Lttw5TAjx4Qapr/JNFZCTk
snI+4OI765f7A==
=3AHZ
-----END PGP PUBLIC KEY BLOCK-----

### Verifying Red Hat Signed Packages

Having installed Red Hat's GPG keys, we can then verify official Red Hat packages as being authentic. As an example, let's verify the Lynx package that we looked at earlier:

```bash
# rpm -K lynx-2.8.5-11.i386.rpm
lynx-2.8.5-11.i386.rpm: (sha1) dsa sha1 md5 gpg OK
```

If all goes well you will see an `MD5 gpg OK` message. This proves that the signature of the package has been verified and that it has not been corrupted or altered.

### Installing Packages

RPM provides other advantages over the Package Management Tool, as it can install packages from *any* source – including Red Hat distribution CDs, network locations, FTP, and HTTP.

The syntax for installing a package looks like this:

```bash
rpm -i [options] <package_filename>
```

As an example, let's look at the installation of a couple of packages, and their dependencies, now.

#### **Try It Out**

**Installing Packages using RPM**

- 1. First, let's install the Lynx web browser that we've just verified is OK. You should already be logged in with root privileges, with the terminal window open and still in the `Red Hat/RPMS` directory of your mounted CDROM. From there, type in the following at the command line:

```bash
# rpm -ivh lynx-2.8.5-11.i386.rpm
```

The output you get depends on whether the Lynx browser is already installed. If it's not, then you'll see the following:

```text
Preparing...                ################################################## [100%]
 1:lynx                     ################################################## [100%]
```

But, if it's already on your machine then RPM won't attempt to install it again. Instead, you will get the following message:

```text
Preparing...                ################################################## [100%]
    package lynx-2.8.5-11 is already installed
```

- 2. That went quite easily, didn't it? Now, let's perform another installation example, installing a package that has dependencies. The **balsa** package is a GNOME e-mail client. If we try to install this using the same technique as we did before, we get a failed dependencies error message. Try it if you like:

```bash
# rpm -ivh balsa-2.0.6-1.i386.rpm
error: Failed dependencies:
 libesmtp.so.5 is needed by balsa-2.0.6-1
```

- 3. As you can see from the output, RPM fails to install the package. Instead, it shows an error message indicating that the package balsa-2.0.6-1.i386.rpm has a dependency that is not met – namely, the package libesmtp.so.5 is not installed. RPM provides the file name of the dependency but does not provide the package name to resolve it. This isn't very helpful, but fortunately Red Hat provides an extra package that can be installed to get suggestions about package filenames to resolve dependencies.

The package in question is currently called rpmdb-redhat-9-0.20030313.i386.rpm but the name may differ slightly in your version (just look on your CDROM for a filename beginning rpmdb- and that'll be it). Simply install it as you installed the previous packages:

```bash
# rpm -ivh rpmdb-redhat-9-0.20030313.i386.rpm
Preparing...                  ########################################### [100%]
1:rpmdb-Red Hat            ########################################### [100%]
```

- 4. Now if we try to install the balsa package again we will get a message suggesting the location of the dependent file:

```bash
# rpm -ivh balsa-2.0.6-1.i386.rpm
error: Failed dependencies:
    libesmtp.so.5 is needed by balsa-2.0.6-1
Suggested resolutions:
    libesmtp-0.8.12-5.i386.rpm
```

- 5. So, let's try again. This time, install the suggested package libesmtp-0.8.12-5.i386.rpm first:

```bash
# rpm -ivh libesmtp-0.8.12-5.i386.rpm
Preparing...                  ########################################### [100%]
1:libesmtp                ########################################### [100%]
```

- 6. When that's complete, you can install the balsa package as follows:

```bash
# rpm -ivh balsa-2.0.6-1.i386.rpm
Preparing...                  ########################################### [100%]
1:balsa                   ########################################### [100%]
```

Alternatively, you could have installed them together on the same line, like this:

```bash
# rpm -ivh balsa-2.0.6-1.i386.rpm libesmtp-0.8.12-5.i386.rpm
Preparing...                  ########################################### [100%]
1:libesmtp                ########################################### [ 50%]
2:balsa                   ########################################### [100%]
```

- 7. Finally, it's worth mentioning that RPM packages can be installed directly from the Internet. We can use HTTP or FTP addresses to install directly. If you wanted to install say the vnc-server directly from the Red Hat web site, you'd type this:

```bash
# rpm -ivh
http://ftp.redhat.com/pub/redhat/linux/9/en/os/i386/RedHat/RPMS/vnc-server-3.3.3r2-47.i386.rpm
```

### How It Works

We've used the RPM command for installation, much as we did for querying earlier, this time, however, the options are slightly different. Each of the three install commands used the option -ivh here, which translates as follows:

- i indicates that we intend to perform an installation
- v indicates that we want RPM to display "additional information". For example to display package file names while performing multiple package installation with one rpm command.
- h indicates that we want RPM to print hash (#) marks during the installation process to show the progress of the installation.

### Removing Packages

Removing unwanted packages from your system is an important task. RPM makes package removal easy. It keeps record of all the files installed by each package, so we can easily clean our system by removing all the files associated with an unwanted package.

### Try It Out

**Removing Packages using the RPM**

OK, so we probably don't actually need the vnc-server, lynx, and balsa packages on our system. So, here's how we go about removing them:

- 1. First, type the following to remove the vnc-server package:

```bash
# rpm -e vnc-server
```
