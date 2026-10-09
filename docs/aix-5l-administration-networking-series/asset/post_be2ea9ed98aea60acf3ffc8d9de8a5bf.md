
3. `# mksysb /dev/rmt0` Create backup.
4. `# chdev -l rmt0 -a block_size=<blocksize>` Reset tape block size.

# DISTRIBUTED SYSTEM INSTALLATION

If installing or updating a single system isn’t problem enough, think about repeating the process over and over again in a multisystem environment! In many cases, these systems represent both disk and nondisk configurations.

# NFS Installation Support

In networked environments with existing AIX systems, copy product and maintenance images to a file system, /inst.images. NFS export this file system to each of the remote sites. This method requires repeating the installation process on each machine. It provides the capability of individually tailoring the update on each system.

# Creating a Reference System

To minimize the amount of time and work required to update multiple disk systems, create a single reference system image that can be cloned on each machine.

1. Update and tailor one system that represents your base configuration.
2. List the file systems that you do not want to back up in the `/etc/exclude.rootvg` file and run the `mksysb` with the `-i` and `-e` options.

   ```bash
   # echo /inst.images >> /etc/exclude.rootvg
   # mksysb -i -e /inst.images/image_name
   ```

3. In nonnetworked environments, direct `mksysb` output to portable media. If network access is available, direct the output image to a file system, /inst.images.
4. Create a Network Install Manager in networked environments with NFS and TCP/IP support.

# Network Install Manager (NIM)

Network Install Manager (NIM) facilitates central management of software installation and maintenance across all AIX machines participating in a distributed networked environment. How was that statement for an intro? NIM can also customize, boot, and run diagnostics remotely on each of the NIM-managed workstations. NIM is either IP-based, using the BOOTP, TFTP, and NFS protocols to distribute boot images and software to each NIM client. NIM can be used over any network that supports the TCP/IP protocol and can support multiple network interface types on the central server. As you might guess, NIM is a very complex tool, but there is an Easy Setup SMIT option that uses the most common setup for configuration, `smitty nim_config.env`. The Easy Setup is great, but we need to add in more details for the novice to get started.

1. First, create a `/tftpboot` filesystem before running `smitty nim_config.env`.
   To create the `/tftpboot` filesystem and install the NIM software, use the following command sequence:

   ```bash
   # mkivs -y 'lv' rootvg 1
   # crfs -v jfs -d lv -m /tftpboot -A yes
   # mount /tftpboot
   # chfs -a size=120000 /tftpboot
   # df -k /tftpboot
   # installp -qaX -d <device> bos.sysmgt.nim.master
   bos.sysmgt.nim.spot
   # smitty nim_config.env
   ```

2. Create a `/tftpboot` filesystem and install the NIM filesets using the preceding command sequence.

   ![](img/82f851021955589d82b22750fb3b1646_124_0.png)

3. Configure the NIM Master from CD-ROM using `smitty nim_config.env`.

   ![](img/82f851021955589d82b22750fb3b1646_125_0.png)

4. Define the client machine(s) using `smitty nim_mac`.
5. Create a `mksysb` image and define a `mksysb` resource using `smitty nim_res`.
6. Install a stand-alone client from the `mksysb` image using `smitty nim_bosinst`.
7. Boot the client.

   ![](img/82f851021955589d82b22750fb3b1646_125_1.png)

An NIM environment is composed of two system types: an NIM master and one or more NIM clients. An NIM master centrally orchestrates all the management functions for the NIM clients in the network. The master server must be a stand-alone workstation with sufficient storage resources to provide boot images and shared product object trees (SPOT) for all managed clients. The NIM master server must be installed with the AIX network and spmgr filesets required for NIM operation. There is only one NIM master per set of clients. NIM clients may be any mixture of diskless, stateless, and stand-alone workstations with network connectivity to the NIM master.

NIM supports three types of clients:

- **Stand-alone**: Machines with local copies of AIX and LPPs
- **Diskless**: Network filesystems, paging, and dump; bootstrap ROM for network boot
- **Stateless**: Network filesystems; local paging and dump; bootstrap ROM for network boot; better performance than diskless configuration

The AIX filesets that make up NIM support are bundled in `bos.sysmg`. The `bos.sysmg.nim.master` fileset is used to build the NIM master server. The `bos.sysmg.nim.client` fileset is installed on each of the stand-alone NIM clients. The fileset `bos.sysmg.nim.spot` is used to create SPOT filesets for NIM diskless and stateless client types.

The NIM master stores information required to identify each managed client and network type as an object in an ODM database. This is where most of the difficulty comes in managing a NIM environment. Commands are supplied to list, update, and verify NIM ODM objects and relationships; but in practice, fending with the ODM is not quite as straightforward as working with human-readable tables. The NIM master must maintain relationships that link machine objects to network objects, network objects to network objects (routing), and machine objects to machine objects. Common NIM commands used to update and verify NIM ODM objects and relationships include `nim`, `nimconfig`, `nimrelclient`, and `lsnim`.

My recommendation is that you use SMIT to configure and manage NIM; you can use the Web-based System Manager, but it is a java pig and is very slow to use. The SMIT panels do a much better job in reminding you of all the attributes that must be associated with NIM objects to ensure that proper object-to-object relationships are maintained. Go ahead and use `lsnim` to do a quick check of ODM contents, but use SMIT to do the rest. I'll use SMIT in the following treatment of setting up an NIM environment.

# For Information and Support

- 1-800-CALL-AIX
- 1-800-IBM-4FAX
- 1-800-237-5511

# For Problem Support

| Command | Description |
|---|---|
| `IBMink.advantis.com` | Internet telnet `IBMLink` |

# For Maintenance Level and History

| Command | Description |
|---|---|
| `oslevel` | AIX `3.2.4+` version and release level |
| `uname -v -r` | Display version and release level |
| `lslpp -a -h <product>` | List maintenance history |

# For Packaging

| Command | Description |
|---|---|
| Fileset | Specific function software set |
| Package | Common function filesets |
| Licensed product | Distribution package sets |
| Bundle | Group of filesets, packages, and maintenance |

# For Backup rootvg

| Command | Description |
|---|---|
| `mksysbfile` | Create image.data file for `mksysb` |
| `mksysb /dev/rmt0/<t>` | Back up rootvg to tape |

# For Maintenance Installation

| Command | Description |
|---|---|
| `smit install` | Base install panel |
| `smit install_latest` | Selective install panel |
| `smit install_all` | Install ALL products |
| `bfbcreate -qv -d <media> -f <disk-path>` | Copy maint to disk |
| `installp -qa -d <media-path> -X all` | APPLY updates |
| `installp -r8 -X all` | REJECT updates |
| `installp -c -g -X all` | COMMIT updates |
| `installp -u <fileset>` | DEINSTALL a fileset |
| `installp -C <fileset>` | CLEAN UP failed install |

# For NIM

| Command | Description |
|---|---|
| `smit nimconfig` | Configure and start NIM master |
| `smit nim_mknet` | Create NIM network objects |
| `smit nim_mkroute` | Define NIM network routes |
| `smit nim_mkmac` | Create client network object |
| `smit nim_mkres` | Create lpp_source |
| `smit nim_alloc` | Create bos.inst resources |
| `lsnim` | List NIM-defined objects |
| `bootinfo -q` | Check IPL ROM emulation |
| `bosboot -r` | Create IPL ROM media |
| `smit nim_alloc` | Create bos_inst resource on client |
| `smit nim_perms` | Set master push permission |
| `smit nim_mac_op` | Select client and resource |
| `smit nim_mkgrp` | Create a NIM client group |
| `smit bos_inst` | Push install stand-alone client |
| `smit nim_install` | Pull install from client |
| `smit dksl_init` | Initialize diskless client |
| `smit nim_mac_op lpchck` | Verify installation |
| `smit nim_backup_db` | Back up NIM configuration |
| `smit nim_restore_db` | Restore NIM configuration |
| `smit nim_client_op` | Remotely operate a NIM client |
| `smit nim_unconfig` | Unconfigure NIM master |

# CHECKLIST

The following is a checklist for the key points in installation and maintenance:

- Follow the installation guide carefully each time you install AIX.
- Configure operating system and production filesystem configuration to get the best performance from the disk space.
- Preinstall parts of the basic operating system (BOS) and product runtime environments on the system, if you are installing a brand new P-Series or RISC System/6000.
- Manage the installation of the Licensed Program Products (LPP) by using the SMIT install FastPath or by using the `installp` command.
- Monitor the installation of non-LPP products.
- When you do not need an application on the system, you can remove it through the SMIT software maintenance utilities.
- Apply maintenance level (ML) patches.
- Set default system and environment variables for a new installation.
- Identify distributed system installation procedures.
- Identify DocSearch keywords.
- Identify software install / maintenance information and support procedures.
