server is identified.

+   - For Samba domain controllers, check to see that the `netlogin` share has been defined. Validate using `smbclient -U` to test authentication.

# Shares

Assuming that authentication problems aren't keeping you from accessing a share, the most likely culprit is access control. Carefully substantiate that you haven't blocked client access due to global `hosts deny` restrictions. Are read-write permissions being applied the way you expect?

To verify general access, use `smbclient` to connect a common share like a home directory defined by the `[homes]` section in `smb.conf` (Example 15.13). Any share will do. Invoke `smbclient` with the share name. If the share requires authentication, you should be prompted for a password. Once the share is authenticated, you should have access to it.

# Example 15.13 Samba Home Share Access

```
$ smbclient //wizard/deroest
Password:
Domain = [EYRIE] OS = [Unix] Serve r= [Samba 2.0.5a]
Smb: \>
```

Also try connecting the share from a Windows client using the **NET USE** command or **Windows Explorer → Tools → Map a Network Device** (Figure 15.3).

```
C:\NET USE J: \\ <server NetBIOS name>\<share name>
```

In the case of printer shares, make sure that you have correctly identified `printcap` printers and that they are marked as `printable`. Next confirm that the `printing os` type is set and that it corresponds to the `print command` and `lpq command` parameters.

If you are providing downloadable Windows 9x printer drivers, verify that the `printer driver name` and `printer driver location` directory are correct and readable. The `printer driver name` is case sensitive and must exactly match the name expected by the Windows driver install procedure. Always print a test page as part of the Windows network printer driver install to make sure features like fonts and colors are working as expected.