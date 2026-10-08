# 276

The following example uses the -k option to display the output for the same directory
1024-byte blocks.

```
paperback@ du -k /export/home/winsor/Docs
j3726 /export/home/winsor/Docs
paperback@
```

The following example uses the -h option to display the output for the
/export/home/winsor/Man-9 directory.

```
mopoke% du -h /export/home/winsor/Man-9
1.5M /export/home/winsor/Man-9
mopoke%
```

# Usage

largefile(5) for the description of the behavior of du when encountering
greater or equal to 2 Gbytes (2**31 bytes).

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the
execution of du: LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status

+   0 Successful completion.
>0 An error occurred.

# Attributes

attributes(5) for descriptions of the following attributes.

```
/usr/bin/du
```

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwcu |
| CSI | Enabled |
| Interface Stability | Stable |

```
/usr/xpg4/bin/du
```

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwcu4 |
| CSI | Enabled |
| Interface Stability | Standard |

# See Also

ls(1), stat(2), attributes(5), environ(5), fsattr(5), largefile(5),
XPG(4)

System Administration Guide: Basic Administration