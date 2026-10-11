
## FOR FURTHER READING

### On-Line Documentation

The following list represents the documentation that comes with Tripwire.

- /usr/doc/tripwire-1.2/Changelog
- /usr/doc/tripwire-1.2/FAQ
- /usr/doc/tripwire-1.2/INTERNALS
- /usr/doc/tripwire-1.2/README
- /usr/doc/tripwire-1.2/README.FIRST
- /usr/doc/tripwire-1.2/Readme
- /usr/doc/tripwire-1.2/TODO
- /usr/doc/tripwire-1.2/WHAT'SNEW
- /usr/doc/tripwire-1.2/docs
- /usr/doc/tripwire-1.2/docs/README
- /usr/doc/tripwire-1.2/docs/appdev.txt
- /usr/doc/tripwire-1.2/docs/design.doc.ps
- /usr/doc/tripwire-1.2/docs/sans.txt
- /usr/man/man5/tw.config.5
- /usr/man/man8/siggen.8
- /usr/man/man8/tripwire.8

### Web Site

The following web resource contains additional information about Tripwire.

http://www.tripwiresecurity.com/

## Space, the Cracker Frontier

### The Cryptographic and Transparent Cryptographic Filesystems

Encryption is a wonderful thing. In a day and age when you never can be sure who’s accessing your system, the ability to protect your data through encryption can help you sleep at night. In this chapter we will explore two publicly available tools—the Cryptographic File System (CFS) and the Transparent Cryptographic File System (TCFS)—that will assist you in securing your data.

Both of these utilities operate based on the NFS client-server model, so you will need to make sure that NFS client and server functionality are available on appropriate systems.

#### OVERVIEW OF THE CRYPTOGRAPHIC FILE SYSTEM

We will take a look at CFS first as it is at the heart of TCFS. In *CFS and TCFS Comparison* on page 431 we will consider the differences between the two.

Unlike PGP, which is capable of encrypting data on a *per-file* basis, CFS provides a mechanism to encrypt directories and their contents through the standard UNIX filesystem interface. In this way, CFS allows for the encryption of files and directories through almost any filesystem, including the Linux ext2 filesystem and NFS. CFS never stores any cleartext on disk, nor does it ever forward any cleartext over the network.

Users create and access their encrypted directories through the use of a passphrase, which is used to generate the cryptographic key (or keys) for user-chosen cryptographic algorithm. Once the CFS directory is created, users may access it with the cftattach command and their passphrase. Everything created inside the CFS directory will be encrypted transparently to the user.

From a system-administrative perspective, the initial setup of CFS is quite simple and is described in CFS Administrative Tasks on page 408. The major impact of CFS is on performance related to active reads and writes to CFS resources that require decryption and encryption (backups and restores; for example, capturing and recovering CFS resources in their encrypted state). In environments in which multiple simultaneous access to CFS is anticipated, systems should be configured with copious amounts of memory and high-speed processors. Alternatively, such environments may well benefit from TCFS instead, which is discussed in Overview of TCFS on page 416.

### CFS Flow of Events

The CFS implementation is not compiled. Figure 15.1 shows the way in which an application passes read/write requests to the CFS daemon (cfasd) for decryption and encryption services.

The application actually knows nothing about CFS as it is dealing with a local directory. If local directory simply happens to be an NFS mount point (attached to cfsd through the localhost (loopback interface) at port 3049 (by default). The cfsd acts as both an NFS server, which responds to client requests through the mount point (normally /crypt), and the encryption engine (through a system call). The filesystem treats the read/write requests from cfsd as it would any other read/write request. Thus, the encryption/decryption mechanism is completely transparent to users and the kernel.

Now let’s look at obtaining and installing CFS.

### OBTAINING AND INSTALLING CFS

CFS was written by Matt Blaze (copyright AT&T). It is freely available, but is subject to the United States export control laws. See the README.install file in your build directory for more details.

At the time of this writing, the latest version of CFS is 1.4.0beta2. It is available in the United States and Canada at

http://cryptography.org/

where you will have to first certify that you are a citizen or permanent resident of the United States or Canada. Then you will be allowed access to the download page (which changes regularly).

Version 1.3.3 of CFS is available worldwide at

http://www.replay.com/redhat/cfs.html

![](img/7933c44717ab0711177ea7153f959fc5_448_0.png)

**Fig. 15.1 CFS Flow of Events**

in RPM format. Both source and i386 binary RPMs are there. If you wish to simply install the RPM, check the PGP signature and then execute

```bash
# rpm -ivh cfs-1.3.3-3.i386.rpm
```

You may also install the source RPM similarly.

If you wish to compile the 1.4.beta2 version, you will need to make a number of changes. These changes will allow for compilation on either Red Hat 5.2 or 6.0. First extract the distribution in a build directory (we will use /usr/src/custom/cfs1.4),

```bash
# cd /usr/src/custom/cfs1.4
# tar xzvf cfs-1.4.0.beta2_tar.gz
```

In the *Makefile*, make sure that the flags listed in Example 15-1 are set as shown. Also be sure to comment out the line *cc=you_forget_to_edit_the_makefile*, as shown in Example 15-1.

**Example 15-1 Correct CFS Version 1.4.0beta2 Makefile Entries**

```text
<many lines not shown>
BINDIR=/usr/bin    # For our examples
ETCDIR=/usr/sbin  # For our examples
<many lines not shown>
CC=gcc
COPF=-O2 -DPROTOTYPES=1
<many lines not shown>
CFLAGS=${COPF} -D __STDC__ -D_FILeno -INO -I8(RINCLUFES)
LIBS=
COMPAT=
RPCOFTS=-k -h
#CC=you forgot to edit the makefile
<many lines not shown>
<remainder of file not shown>
```

Next, you will need to apply some corrections to the file *tru*erand.c (see http://www.mit.edu/8008/bloom-picayune/cfs/). In that file, find

```c
longjmp(env, 1);
```

and change it to

```c
siglongjmp(env, 1);
```

Also find

```c
if (setjmp(env))
```

and change it to

```c
if (sigsetjmp(env, 1))
```

Save the changes and close the file. Now run

```bash
# make cfs
# make install_cfs
```

and your compilation and installation should proceed without difficulty.

**NOTE**

> If compilation fails when you run *make cfs*, modify the files *nfsrpc_svr.c* and *nfsproto_svr.c* so that all instances of *xdr_argument* and *xdr_result* are _xdr_argument* and _xdr_result, respectively. Do not globally replace these variables because some instances will already have the leading underscore, _. This step must be performed after the failure of *make cfs*.

Now you are ready to set up CFS.

### CFS Administrative Tasks

After installing CFS (either version), the root user will need to configure CFS for use. The steps are fairly simple and once done may be automated through start-up scripts. The following two sections cover the details.

#### Establishing the Bootstrap Mount Point

**NOTE**

> If you installed CFS by installing `cfs-1.3.3-i386.rpm`, you need to execute only the `exportfs -a` step in this section.

CFS requires a bootstrap mount point for the cleartext directories (called *virtual directories*). You may choose whatever name for this mount point you wish. We will use `/.cfsfs`. Create the directory and set the permissions to null.

```bash
# mkdir /.cfsfs
# chmod 0 /.cfsfs
```

Export this newly created resource by placing the following entry in `/etc/exports`

```text
/.cfsfs      localhost
```

and export the resource with

```bash
# /usr/sbin/exportfs -a
```

At each reboot, this resource will automatically be exported, due to its presence in `/etc/exports`.

Next create the CFS mount point. Again, choose any name. For our examples, we will use `/crypt`.

```bash
# mkdir /crypt
# chmod 755 /crypt
```

At this point, you are ready to make the resource available.

**Running cfsd and Mounting the Bootstrap**

In order to mount the virtual directory `/crypt` to the bootstrap mount point `/.cfsfs`, you first need to run `cfsd`. By default, `cfsd` runs on port 3049, but, if for some reason you cannot allow `cfsd` to run on that port, you may specify the desired port number as an argument; for example, starting it at the default port 3049

```bash
# /usr/sbin/cfsd
```

or at a different port, say 9111,

```bash
# /usr/sbin/cfsd 9111
```

Next, mount the virtual directory to the bootstrap directory.

```bash
# /bin/mount -o port=3049,intr localhost:/.cfsfs /crypt
```

The option `port=3049` is required since by default the `mount` command attempts to communicate with NFS, which listens to port number 2049. You will probably want to automate this process in a start-up script, such as `/etc/rc.d/rc.local`. The script fragment in Example 15-2 will do the trick.
