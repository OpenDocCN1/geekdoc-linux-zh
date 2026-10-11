# #### 2.3.3.1 Example: Engineering Office

The engineering office network server we present here is designed to demonstrate use of the new tdbsam password backend. The tdbsam facility is new to Samba-3. It is designed to provide many user and machine account controls that are possible with Microsoft Windows NT4. It is safe to use this in smaller networks.

# **Example 2.3.7** Engineering Office smb.conf (globals)

```
[global]
  workgroup = MIDEARTH
  netbios name = FRODO
  passdb backend = tdbsam
  printcap name = cups
  add user script = /usr/sbin/useradd -m %u
  delete user script = /usr/sbin/userdel -r %u
  add group script = /usr/sbin/groupadd %g
  delete group script = /usr/sbin/groupdel %g
  add user to group script = /usr/sbin/grouppmod -A %u %g
  delete user from group script = /usr/sbin/grouppmod -R %u %g
  add machine script = /usr/sbin/useradd -s /bin/false -d /var \ 
      /lib/nobody %u
  # Note: The following specifies the default logon script.
  # Per user logon scripts can be specified in the user account using
  pdbedit
      logon script = scripts\logon.bat
  # This sets the default profile path. Set per user paths with
      pdbedit
      logon path = \\%L\Profiles\%u
      logon drive = H:
      logon home = \\%L\%u
      domain logons = Yes
      os level = 35
      preferred master = Yes
      domain master = Yes
      idmap uid = 15000-20000
      idmap gid = 15000-20000
      printing = cups
```

+   1.  A working PDC configuration using the tdbsam password backend can be found in Example 2.3.7 together with Example 2.3.8:

+   2.  Create UNIX group accounts as needed using a suitable operating system tool:

```
root# groupadd ntadmins
root# groupadd designers
root# groupadd engineers
root# groupadd qateam
```