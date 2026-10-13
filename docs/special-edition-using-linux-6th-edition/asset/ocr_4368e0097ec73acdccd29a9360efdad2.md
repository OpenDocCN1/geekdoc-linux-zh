The command brings up the graphical interface shown in Figure 28.7.

**Figure 28.7**  
The nwbotrustees utility window.

![](bbox=[0.207, 0.118, 0.664, 0.353])

After the window opens, you need to perform the following steps to accomplish the desired results:

+   1. Click Add Trustee in the Directory Trustees window.
+   2. Type the username in the New Trustee field.
+   3. Choose the rights that you want to give jsmith by clicking the appropriate check boxes (treat the Change option as the Create Right).
+   4. Click the Add Rights button.

After you have performed these steps, the same command that brought up the graphical interface can be used to modify or remove the rights assigned to jsmith.

# VIEWING NETWARE FILESYSTEM TRUSTEES ASSIGNMENTS AND RIGHTS

The nwboshowtrust utility can be used in one of two ways. You can use it to show directories or files on a server of which the specified object is a trustee, or you can use it to list all trustees of a specific directory or file. The following syntax is used (Table 28.22 shows the possible command-line options for the nwboshowtrust utility):

```
nwboshowtrust [OPTIONS]
```

**Table 28.22 — Command-Line Options for nwboshowtrust**

| Options | Description |
|---|---|
| `-o <OBJECT PATH>` | Specifies the object NetWare automounted path whose rights are being checked (cannot be used with the `-p` option) |
| `-p <PATH>` | Specifies the path of the directory for which to list trustee assignments (cannot be used with the `-o` option) |
| `-h` | Displays command help |