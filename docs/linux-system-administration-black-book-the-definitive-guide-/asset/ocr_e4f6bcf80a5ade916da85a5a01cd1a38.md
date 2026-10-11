+   5. Start with the share name. This name is formatted as follows: [sharename].
+   The name should have no spaces or punctuation. You can use any term
+   except the reserved shares: [global], [homes], and [printers].

+   6. Typically, the first option you set after the print share name is comment.
+   Indent this line under the share name so that it is obvious at a glance where
+   this share definition starts and ends. For example, so far, you might have
+   the following:

```
[laser]
    comment = Main laser printer
```

+   7. Next is often the path option. Here, you set where within the file system all
+   print jobs sent from SMB clients should be spooled to. For example, the
+   definition might now be similar to the following:

```
[laser]
    comment = Main laser printer
    path = /var/spool/samba/laser
```

+   8. Just as with file shares, this is the point at which print shares are no longer
+   consistent. A different set of options from the ones used to configure file
+   shares is of interest to those setting up print shares. Print share options are
+   listed in Table 18.7. Examine this list carefully.

**Table 18.7 Popular options used in individual Samba share definitions.**

| Option | Purpose | Value(s) | Example |
| :--- | :--- | :--- | :--- |
| lppause command | Sets the command used to either halt printing or halt spooling for a print job. | The path to the script or command to run, plus the substitution variables %p to refer to a specific printer and %j to refer to a specific job number | lppause = /usr/bin/lp -l -%p-%j -H hold |
| lpq command | Sets the command used to display print queue information for a specific printer. | The path to the script or command to run, plus the %p substitution variable to refer to a specific printer | lpq command = /usr/bin/lpq %p |