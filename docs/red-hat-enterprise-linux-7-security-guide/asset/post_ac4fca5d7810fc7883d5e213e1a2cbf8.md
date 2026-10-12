
The SCAP Security Guide (SSG) project's package, scap-security-guide, contains the latest set of security policies for Linux systems. To install the SCAP Security Guide package on your system, enter the following command as root:

```bash
# yum install scap-security-guide
```

A part of scap-security-guide is also a guidance for Red Hat Enterprise Linux 7 settings. To inspect the security content available with scap-security-guide, use the **oscap info** module:

```bash
$ oscap info /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

The output of this command is an outline of the SSG document and it contains available configuration profiles. To audit your system settings, choose a suitable profile and run the appropriate evaluation command. For example, the following command is used to assess the given system against a draft SCAP profile for Red Hat Certified Cloud Providers:

```bash
$ oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_rht-ccp --results ssg-rhel7-xccdf-result.xml --report ssg-rhel7-report.html /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

## 7.10. Additional Resources

For more information about various security compliance fields of interest, see the resources below.

### Installed Documentation

- oscap(8) – The manual page for the **oscap** command-line utility provides a complete list of available options and their usage explanation.
- scap-workbench(8) – The manual page for the **SCAP Workbench** application provides a basic information about the application as well as some links to potential sources of SCAP content.
- scap-security-guide(8) – The manual page for **scap-security-guide** provides further documentation about the various available SCAP security profiles. Examples how to utilize the provided benchmarks using the **OpenSCAP** utility are provided as well.

### Online Documentation

- [The OpenSCAP project page](#) – The home page to the OpenSCAP project provides detailed information about the **oscap** utility and other components and projects related to SCAP.
- [The SCAP Workbench project page](#) – The home page to the SCAP Workbench project provides detailed information about the **scap-workbench** application.
- [The SCAP Security Guide (SSG) project page](#) – The home page to the SSG project that provides the latest security content for Red Hat Enterprise Linux.
- [National Institute of Standards and Technology (NIST) SCAP page](#) – This page represents a vast collection of SCAP related materials, including SCAP publications, specifications, and the SCAP Validation Program.
- [National Vulnerability Database (NVD)](#) – This page represents the largest repository of SCAP content and other SCAP standards based vulnerability management data.
- Red Hat OVAL content repository – This is a repository containing OVAL definitions for Red Hat Enterprise Linux systems.
- MITRE CVE – This is a database of publicly known security vulnerabilities provided by the MITRE corporation.
- MITRE OVAL – This page represents an OVAL related project provided by the MITRE corporation. Among other OVAL related information, these pages contain the latest version of the OVAL language and a repository of OVAL content with thousands of OVAL definitions.
- Red Hat Satellite documentation – This set of guides describes, among other topics, how to maintain system security on multiple systems by using OpenSCAP.

# CHAPTER 8. FEDERAL STANDARDS AND REGULATIONS

In order to maintain security levels, it is possible for your organization to make efforts to comply with federal and industry security specifications, standards and regulations. This chapter describes some of these standards and regulations.

## 8.1. Federal Information Processing Standard (FIPS)

The Federal Information Processing Standard (FIPS) Publication 140-2 is a computer security standard, developed by the U.S. Government and industry working group to validate the quality of cryptographic modules. See the official FIPS publications here: [http://csrc.nist.gov/publications/PubsFIPS.html](http://csrc.nist.gov/publications/PubsFIPS.html).

The FIPS 140-2 standard ensures that cryptographic tools implement their algorithms properly. See the full FIPS 140-2 standard at [http://dx.doi.org/10.6028/NIST.FIPS.140-2](http://dx.doi.org/10.6028/NIST.FIPS.140-2) for further details on these levels and the other specifications of the FIPS standard.

To see the complete list of all FIPS 140-2 certificates, visit [http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/140val-all.htm](http://csrc.nist.gov/groups/STM/cmvp/documents/140-1/140val-all.htm). To learn about compliance requirements, see [the Red Hat Government: Standards page](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/.../).

### 8.1.1. Enabling FIPS Mode

To make Red Hat Enterprise Linux compliant with the Federal Information Processing Standard (FIPS) Publication 140-2, you need to make several changes to ensure that accredited cryptographic modules are used. You can either enable FIPS mode during system installation or after it.

#### During the System Installation

To fulfill the *strict FIPS 140-2 compliance*, add the `fips=1` kernel option to the kernel command line during system installation. With this option, all keys' generations are done with FIPS-approved algorithms and continuous monitoring tests in place. After the installation, the system is configured to boot into FIPS mode automatically.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_238_0.png)

> **IMPORTANT**
> Ensure that the system has plenty of entropy during the installation process by moving the mouse around or by pressing many keystrokes. The recommended amount of keystrokes is 256 and more. Less than 256 keystrokes might generate a non-unique key.

#### After the System Installation

To turn the kernel space and user space of your system into FIPS mode after installation, follow these steps:

1.  Install the dracut-fips package:

    ```bash
    ~]# yum install dracut-fips
    ```

    For CPUs with the AES New Instructions (AES-NI) support, install the dracut-fips-aesni package as well:

    ```bash
    ~]# yum install dracut-fips-aesni
    ```

2.  Regenerate the initramfs file:

    ```bash
    ~/# dracut -v -f
    ```

    To enable the in-module integrity verification and to have all required modules present during the kernel boot, the initramfs file has to be regenerated.

    > **WARNING**
    > This operation will overwrite the existing initramfs file.

3.  Modify boot loader configuration.

    To boot into FIPS mode, add the `fips=1` option to the kernel command line of the boot loader. If your /boot or /boot/EFI/ partitions reside on separate partitions, add the `boot=<partition>` (where <partition> stands for /boot or /boot/EFI) parameter to the kernel command line as well.

    To identify the boot partition, enter the following command:

    ```bash
    ~/ $ df /boot
    Filesystem     1K-blocks    Used Available Use% Mounted on
    /dev/sda1       495844    53780   416464  12% /boot
    ```

    To ensure that the `boot=` configuration option works even if the device naming changes between boots, identify the universally unique identifier (UUID) of the partition by running the following command:

    ```bash
    ~/ $ blkid /dev/sda1
    /dev/sda1: UUID="05c000f1-f899-467b-a4d9-d5ca4424c797" TYPE="ext4"
    ```

    Append the UUID to the kernel command line:

    ```text
    boot=UUID=05c000f1-f899-467b-a4d9-d5ca4424c797
    ```

    Depending on your boot loader, make the following changes:

    -   **GRUB 2**

        Add the `fips=1` and `boot=<partition of /boot or /boot/EFI>` options to the `GRUB_CMDLINE_LINUX` key in the `/etc/default/grub` file. To apply the changes to `/etc/default/grub`, rebuild the `grub.cfg` file as follows:

        -   On BIOS-based machines, enter the following command as root:

            ```bash
            ~/# grub2-mkconfig -o /etc/grub2.cfg
            ```

        -   On UEFI-based machines, enter the following command as root:

            ```bash
            ~]# grub2-mkconfig -o /etc/grub2-efi.cfg
            ```

    -   **zipl** (on the IBM z Systems architecture only)

        Add the `fips=1` and `boot=<partition of /boot>` options to the `/etc/zipl.conf` file to the kernel command line and apply the changes by running the following command as `root`:

        ```bash
        ~]# zipl
        ```

4.  Make sure prelinking is disabled.

    For proper operation of the in-module integrity verification, prelinking of libraries and binaries has to be disabled. Prelinking is done by the `prelink` package, which is not installed by default. Unless `prelink` has been installed, this step is not needed. To disable prelinking, set the `PRELINKING=no` option in the `/etc/sysconfig/prelink` configuration file. To disable existing prelinking on all system files, use the `prelink -u -a` command.

5.  Reboot your system.

### Enabling FIPS Mode in a Container

A container can be switched to FIPS140-2 mode if the host is also set in FIPS140-2 mode and one of the following requirements is met:

-   The `dracut-fips` package is installed in the container.
-   The `/etc/system-fips` file is mounted on the container from the host.

## 8.2. National Industrial Security Program Operating Manual (NISPOM)

The NISPOM (also called DoD 5220.22-M), as a component of the National Industrial Security Program (NISP), establishes a series of procedures and requirements for all government contractors with regard to classified information. The current NISPOM is dated February 28, 2006, with incorporated major changes from March 28, 2013. The NISPOM document can be downloaded from the following URL: `http://www.nispom.org/NISPOM-download.html`.

## 8.3. Payment Card Industry Data Security Standard (PCI DSS)

From `https://www.pcisecuritystandards.org/about/index.shtml`: *The PCI Security Standards Council is an open global forum, launched in 2006, that is responsible for the development, management, education, and awareness of the PCI Security Standards, including the Data Security Standard (DSS).*

You can download the PCI DSS standard from `https://www.pcisecuritystandards.org/security_standards/pci_dss.shtml`.

## 8.4. Security Technical Implementation Guide

A Security Technical Implementation Guide (STIG) is a methodology for standardized secure installation and maintenance of computer software and hardware.

See the following URL for more information on STIG: `http://iase.disa.mil/stigs/Pages/index.aspx`.
