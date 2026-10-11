```
# First assign well known groups
net groupmap modify ntgroup="Domain Admins" unixgroup=ntadmins
net groupmap modify ntgroup="Domain Users" unixgroup=users
net groupmap modify ntgroup="Domain Guests" unixgroup=nobody

# Now for our added Domain Groups
net groupmap add ntgroup="Designers" unixgroup=designers type=d
net groupmap add ntgroup="Engineers" unixgroup=engineers type=d
net groupmap add ntgroup="QA Team" unixgroup=qateam type=d
```

5. Create the scripts directory for use in the [NETLOGON] share:

```
root# mkdir -p /var/lib/samba/netlogon/scripts
```

Place the logon scripts that will be used (batch or cmd scripts) in this directory.
The above configuration provides a functional PDC system to which must be added file shares and printers as required.

# 2.3.3.2 A Big Organization

In this section we finally get to review in brief a Samba-3 configuration that uses a Lightweight Directory Access (LDAP)-based authentication backend. The main reasons for this choice are to provide the ability to host primary and Backup Domain Control (BDC), as well as to enable a higher degree of scalability to meet the needs of a very distributed environment.

**The Primary Domain Controller** This is an example of a minimal configuration to run a Samba-3 PDC using an LDAP authentication backend. It is assumed that the operating system has been correctly configured.

The Ideals scripts (or equivalent) are needed to manage LDAP-based POSIX and/or SambaSampAccounts. The Ideals scripts may be downloaded from the Idealx2 Web site. They may also be obtained from the Samba tarball. Linux distributions tend to install the Ideals scripts in the /usr/share/doc/packages/sambaXXXXXX/examples/LDAP/smbldap-tools directory. Ideals scripts version smbldap-tools-0.9.1 are known to work well.

+   1. Obtain from the Samba sources ~/examples/LDAP/samba.schema and copy it to the /etc/openldap/schema/ directory.
+   2. Set up the LDAP server. This example is suitable for OpenLDAP 2.1.x. The /etc/openldap/slapd.conf file. Example slapd.conf File

```
# Note commented out lines have been removed
include /etc/openldap/schema/core.schema
include /etc/openldap/schema/cosine.schema
```

+   <http://www.idealx.org>