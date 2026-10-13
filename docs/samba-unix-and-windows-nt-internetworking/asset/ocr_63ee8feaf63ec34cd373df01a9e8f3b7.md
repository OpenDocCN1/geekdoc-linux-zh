![](bbox=[0.14, 0.12, 0.87, 0.54])

Figure 10.7: Windows 2000 domain tree structure

It is still a bit early to tell how Samba can participate in the Windows 2000 domain, tree, and forest model. Keep an eye on the Samba discussion archives concerning the latest Windows 2000 and Samba interoperability issues.

# Summary

+   - Domains are similar to workgroups but provide additional functionality and security via a shared security policy.
+   - Samba supports full domain client compatibility and domain controller services for Windows 9x environments.
+   - To configure Samba as a domain client:

+   1. Stop `smbd` and `nmbd`.
+   2. Update `smb.conf`.

```
security = domain
netbios name = <NetBIOS name>
workgroup = <domain name>
password server = <PDC BDC1 ... BDCn>
encrypt passwords = true
```