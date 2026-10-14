| Table 8.9 Default Windows 2000 Shares |
| Share Name | Description |
| ADMINS$ | Shared for administrative purposes, especially remote management of the server or workstation. |
| IPC$ | Shared for inter-process communication. Connections to an SMB server share are initially negotiated over the IPC$ share. |
| C$, D$, etc. | The root of each logical drive is shared for administrative purposes, including remote management. |

# ADMINISTRATIVE AND DEFAULT SHARES

Windows 2000 includes several default shares for both administrative and system purposes. Various default shares are described in Table 8.9.

> Do not modify the default Windows 2000 shares to avoid leaving your system unstable.

# UNIX SMB Services

In heterogeneous network environments, it is important to provide SMB services to and from UNIX systems. With the exception of Linux, none of the standard UNIX systems ship with any SMB service. Red Hat Linux includes a later build of SAMBA. SAMBA has quickly become the foremost SMB service for UNIX systems.

# SAMBA

SAMBA provides both client and server SMB services for UNIX systems. The great advantage to this is having a unified filesystem for a user's UNIX and Windows 2000 home directories. SAMBA allows SMB connections to and from any supported UNIX platform. We will leave the actual installation of SAMBA as an exercise for the reader. SAMBA includes extensive documentation detailing the compilation and installation processes. Rather than regurgitate the SAMBA documentation, we will simply offer you what we feel to be the "best" configuration and describe the relevant features.