
```
# /usr/sbin/lmfsetup
Register PAK (type q or quit to exit) [template]
    Issuer : dec
    Authorization Number : ala-ng-xxxxxx-xxxx
    Product Name : tcs-ua
    Producer : dec
    Number of units : 1050
    Version :
    Product Release Date :
    Key Termination Date :
    Availability Table Code : h
    Activity Table Code :
    Key Options : mod_units,alpha
    Product Token :
    Hardware-Id :
    Checksum : 2-wwww-xxxx-yyyy-zzzz
PAK registered for template successfully
Register PAK (type q or quit to exit) [template] q

You have registered at least one new PAK. Until it is loaded by use of the lmf reset, lmf load for each newly registered PAK, or rebooting your system, software dependent on them will be treated as if the registrations had not been performed.

Would you like a lmf reset to be performed at this time? [Yes] Yes
```

Let’s now verify that the license PAK for TruCluster Server is loaded and active. To do this we use the lmf(8) command.

```
$ /usr/sbin/lmf list for tcs-ua
TCS-UA                active                unlimited
```

## 10.2.2 Install the TruCluster Server Software

Please note that while it is a good practice to load the TruCluster Server License PAK prior to installing the TruCluster Server software subsets, it is not required. The TruCluster Server software subsets may be installed without the TruCluster Server License PAK, but you will not be able to use any of these software subsets without the License PAK being active.

Now let’s go ahead and install the TruCluster Server software subsets.

- First let’s mount the Tru64 UNIX Associated Products Volume 2 CD-ROM. This contains the TruCluster Server software subsets.

```
$ mount -r /dev/disk/cdrom0c /mnt
```

- Now let’s “cd” to the *TruCluster Server* kit and see what we will be installing.

```
# cd /mnt/TruCluster/kit && ls
TCRBASE520      TCRMAN520      TCRMIGRATE520      instrctl/
```

The *TruCluster Server* installation contains three software subsets:

| Software Subset | Description | Contents |
|---|---|---|
| TCRBASE520 | *TruCluster Server* Base Components | All the mandatory components to implement *TruCluster Server*. |
| TCRMAN520 | *TruCluster Server* Reference Pages | Reference Pages. |
| TCRMIGRATE520 | *TruCluster Server* Migration Tools | Migration tools for migrating from *TruCluster* Production Server and *TruCluster* Available Server. This also contains tools that are useful in troubleshooting general cluster related issues. |

- Using the `setld(8)` command, we perform the installation of the *TruCluster Server* software subsets. We chose to install all the *TruCluster Server* subsets, although if you do not plan to perform a migration from *TruCluster* version 1.5 or 1.6 (see Chapter 26), the TCRMIGRATE subset is not necessary.

```
# /usr/sbin/setld -l .

*** Enter subset selections ***

The following subsets are mandatory and will be installed automatically
unless you choose to exit without installing any subsets:

    - TruCluster Base Components

The subsets listed below are optional:

    There may be more optional subsets than can be presented on a single
    screen. If this is the case, you can choose subsets screen by screen
    or all at once on the last screen. All of the choices you make will
    be collected for your confirmation before any subsets are installed.

- TruCluster(TM) Software :
    1) TruCluster Migration Components
    2) TruCluster Reference Pages

Or you may choose one of the following options:
3) ALL mandatory and all optional subsets
4) MANDATORY subsets only
5) CANCEL selections and redisplay menus
6) EXIT without installing any subsets

Estimated free diskspace(MB) in root:293.1 usr:1428.5 var:1200.6
Enter your choices or press RETURN to redisplay menus.
Choices (for example, 1 2 4-6): 3
```

After selecting to install all the TruCluster Server software subsets, we are asked to verify our selection.

```
You are installing the following mandatory subsets:
    TruCluster Base Components
You are installing the following optional subsets:
- TruCluster(TM) Software :
    TruCluster Migration Components
    TruCluster Reference Pages
Estimated free diskspace(MB) in root:293.1 usr:1428.5 var:1200.6
Is this correct? (y/n): y
```

After we verify our selection of software subsets that we want to install, the installation starts.

```
Checking file system space required to install selected subsets:
File system space checked OK.

3 subsets will be installed.
Loading subset 1 of 3 ...
TruCluster Migration Components
    Copying from . (disk)
    Verifying
Loading subset 2 of 3 ...
TruCluster Reference Pages
    Copying from . (disk)
    Verifying
Loading subset 3 of 3 ...
TruCluster Base Components
    Copying from . (disk)
    Verifying

3 of 3 subsets installed successfully.
```
