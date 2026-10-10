
## OPTIONS

- `-v`
    Print version number and exit.
- `-r`
    Display a security descriptor in raw mode. Values such as type and flags are displayed in hexadecimal format, a SID is not mapped to a name.

### NOTES

Kernel support for getcifsql/setcifsql utilities was initially introduced in the 2.6.37 kernel.

### SEE ALSO

(8), (1)

### AUTHOR

Shirish Pargaonkar wrote the getcifsacl program.

The Linux CIFS Mailing list is the preferred place to ask questions regarding these programs.

# GETENT

### NAME

getent - get entries from Name Service Switch libraries

### SYNOPSIS

**getent** [**option**]... *database key*...

### DESCRIPTION

The **getent** command displays entries from databases supported by the Name Service Switch libraries, which are configured in /etc/nsswitch.conf. If one or more key arguments are provided, then only the entries that match the supplied keys will be displayed. Otherwise, if no key is provided, all entries will be displayed (unless the database does not support enumeration).

The *database* may be any of those supported by the GNU C Library, listed below:

- **ahosts**
    When no key is provided, use (3), (3), and (3) to enumerate the hosts database. This is identical to using **hosts**. When one or more key arguments are provided, pass each key in succession to (3) with the address family **AF_UNSPEC**, enumerating each socket address structure returned.
- **ahostsv4**
    Same as **ahosts**, but use the address family **AF_INET**.
- **ahostsv6**
    Same as **ahosts**, but use the address family **AF_INET6**. The call to (3) in this case includes the **AI_V4MAPPED** flag.
- **aliases**
    When no key is provided, use (3), (3), and (3) to enumerate the aliases database.
    When one or more key arguments are provided, pass each key in succession to (3) and display the result.
- **ethers**
    When one or more key arguments are provided, pass each key in succession to (3) and (3) until a result is obtained, and display the result. Enumeration is not supported on **ethers**, so a key must be provided.
- **group**
    When no key is provided, use (3), (3), and (3) to enumerate the group database. When one or more key arguments are provided, pass each numeric key to (3) and each nonnumeric key to (3) and display the result.
- **gshadow**
    When no key is provided, use (3), (3), and (3) to enumerate the gshadow database. When one or more key arguments are provided, pass each key in succession to (3) and display the result.
- **hosts**
    When no key is provided, use (3), (3), and (3) to enumerate the hosts database. When one or more key arguments are provided, pass each key to (3) or (3), depending on whether a call to (3) indicates that the key is an IPv6 or IPv4 address or not, and display the result.
- **initgroups**
    When one or more key arguments are provided, pass each key in succession to (3) and display the result. Enumeration is not supported on **initgroups**, so a key must be provided.
- **netgroup**
    When one *key* is provided, pass the *key* to (3) and, using (3) display the resulting string triple (*hostname*, *username*, *domainname*). Alternatively, three *keys* may be provided, which are interpreted as the *hostname*, *username* and *domainname* to match to a netgroup name via (3). Enumeration is not supported on **netgroup**, so either one or three *keys* must be provided.
- **networks**
    When no *key* is provided, use (3), (3), and (3) to enumerate the networks database.
    When one or more *key* arguments are provided, pass each numeric *key* to (3) and each nonnumeric *key* to (3) and display the result.
- **passwd**
    When no *key* is provided, use (3), (3), and (3) to enumerate the passwd database.
    When one or more *key* arguments are provided, pass each numeric *key* to (3) and each nonnumeric *key* to (3) and display the result.
- **protocols**
    When no *key* is provided, use (3), (3), and (3) to enumerate the protocols database.
    When one or more *key* arguments are provided, pass each numeric *key* to (3) and each nonnumeric *key* to (3) and display the result.
- **rpc**
    When no *key* is provided, use (3), (3), and (3) to enumerate the rpc database. When one or more *key* arguments are provided, pass each numeric *key* to (3) and each nonnumeric *key* to (3) and display the result.
- **services**
    When no *key* is provided, use (3), (3), and (3) to enumerate the services database.
    When one or more *key* arguments are provided, pass each numeric *key* to (3) and each nonnumeric *key* to (3) and display the result.
- **shadow**
    When no *key* is provided, use (3), (3), and (3) to enumerate the shadow database.
    When one or more *key* arguments are provided, pass each *key* in succession to (3) and display the result.

## OPTIONS

- `-s service`, `--service service`
    Override all databases with the specified service. (Since glibc 2.2.5.)
- `-s database:service`, `--service database:service`
    Override only specified databases with the specified service. The option may be used multiple times, but only the last service for each database will be used. (Since glibc 2.4.)
- `-i`, `--no-iddn`
    Disables IDN encoding in lookups for ahosts/(3) (Since glibc-2.13.)
- `-?`, `--help`
    Print a usage summary and exit.
- `--usage`
    Print a short usage summary and exit.
- `-V`, `--version`
    Print the version number, license, and disclaimer of warranty for getent.

## EXIT STATUS

One of the following exit values can be returned by **getent**:

| Exit Value | Description |
| :--- | :--- |
| **0** | Command completed successfully. |
| **1** | Missing arguments, or *database* unknown. |
| **2** | One or more supplied key could not be found in the *database*. |
| **3** | Enumeration not supported on this *database*. |

## SEE ALSO

(5)

## COLOPHON

This page is part of release 4.00 of the Linux man-pages project. A description of the project, information about reporting bugs, and the latest version of this page, can be found at

# GETFACL

### NAME

getfacl - get file access control lists

### SYNOPSIS

```
**getfacl** [-aceEsRLPtpndvh] file ...
```

```
**getfacl** [-aceEsRLPtpndvh] -
```

### DESCRIPTION

For each file, getfacl displays the file name, owner, the group, and the Access Control List (ACL). If a directory has a default ACL, getfacl also displays the default ACL. Non-directories cannot have default ACLs.

If getfacl is used on a file system that does not support ACLs, getfacl displays the access permissions defined by the traditional file mode permission bits.

The output format of getfacl is as follows:

```
# file: somedir/
# owner: lisa
# group: staff
# flags: -s-
user::rwx
user:joe:rwx #effective:r-x
group::rwx #effective:r-x
group:cool:r-x
mask::r-x
other::r-x
default:user::rwx
default:user:joe:rwx #effective:r-x
default:group::r-x
default:mask::r-x
default:other::---
```

Lines 1—3 indicate the file name, owner, and owning group.

Line 4 indicates the setuid (s), setgid (s), and sticky (t) bits: either the letter representing the bit, or else a dash (-). This line is included if any of those bits is set and left out otherwise, so it will not be shown for most files. (See CONFORMANCE TO POSIX 1003.1e DRAFT STANDARD~17 below.)

Lines 5, 7 and 10 correspond to the user, group and other fields of the file mode permission bits. These three are called the base ACL entries. Lines 6 and 8 are named user and named group entries. Line 9 is the effective rights mask. This entry limits the effective rights granted to all groups and to named users. (The file owner and others permissions are not affected by the effective rights mask; all other entries are.) Lines 11—15 display the default ACL associated with this directory. Directories may have a default ACL. Regular files never have a default ACL.

The default behavior for getfacl is to display both the ACL and the default ACL, and to include an effective rights comment for lines where the rights of the entry differ from the effective rights.

If output is to a terminal, the effective rights comment is aligned to column 40. Otherwise, a single tab character separates the ACL entry and the effective rights comment.

The ACL listings of multiple files are separated by blank lines. The output of getfacl can also be used as input to setfacl.

### PERMISSIONS

Process with search access to a file (i.e., processes with read access to the containing directory of a file) are also granted read access to the file’s ACLs. This is analogous to the permissions required for accessing the file mode.
