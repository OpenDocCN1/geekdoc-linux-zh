# Configuration Option Documentation

Samba has hundreds of configuration options. For complete information, search for these three strings on the `smb.conf` man page: “COMPLETE LIST OF GLOBAL PARAMETERS”, “COMPLETE LIST OF SERVICE PARAMETERS”, and “EXPLANATION OF EACH PARAMETER”. All the same information is accessible in the `smb.conf` info page.

# Other Documentation

The `smb.conf` file supports a number of variable substitutions. The `%h` and `%u` substitutions were discussed earlier in this chapter. For a complete list and description of these substitutions, see the `smb.conf` man page for the phrase “VARIABLE SUBSTITUTIONS”.

The `smb.conf` file has several options related to name mangling. Name mangling is a method of interlacing between old DOS 8.3 filename conventions and modern file naming conventions. It also relates to case sensitivity, default case, and the like. To see a complete treatise on the subject, search for the string “NAME MANGLING” in the `smb.conf` man page.

Last but not least, Samba Unleashed provides extremely deep and broad coverage of Samba.

# Using Samba as a Logon Server

Samba can be used to authenticate logons on Windows 9x, NT, and 2000 computers. Windows 2000 must have NetBIOS over TCP/IP enabled to interact with Samba.

This section gives instructions for setting up Samba to authenticate logons on Windows 9x clients. The version of Samba shipped with Red Hat Linux 7 is not well suited to authenticate logons on NT or Win2K hosts. Those hosts require Samba running as a PDC. PDC functionality is best accomplished with the Samba_TNG version of Samba, which can be downloaded from www.samba.org.

Samba can do all of the following:

+   - Replace the Windows client’s logon mechanism with centralized authentication.
+   - Supply a logon script.
+   - Centrally administer per-user Windows profiles.

Windows profiles are beyond the scope of this chapter. You can get profile details from:

+   - Samba Unleashed
+   - `/usr/share/doc/samba-2.0.7/docs/textdocs/PROFILES.txt`
+   - `/usr/share/doc/samba-2.0.7/docs/textdocs/DOMAIN.txt`

![](bbox=[0.87, 0.27, 0.97, 0.4])