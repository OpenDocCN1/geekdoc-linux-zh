# Table 3.4 tripwire Policy File Property Mask Characters (continued)

| Property | Description |
| :------- | :---------- |
| b | Number of blocks allocated |
| a | Access timestamp |
| m | Modification timestamp |
| c | Inode creation/modification timestamp |
| c | Cyclic redundancy check |

The Tripwire Binaries rule instructs *tripwire* to watch the binaries themselves and tag any violation with the highest severity value:

```
```
# Tripwire Binaries

(rulename = "Tripwire Binaries", severity = $(SIG_HI))
{
  $(TWBIN)/sigs    -> $(ReadOnly);
  $(TWBIN)/tripwire    -> $(ReadOnly);
  $(TWBIN)/twadmin    -> $(ReadOnly);
  $(TWBIN)/twprint    -> $(ReadOnly);
}
```
```

The Tripwire Data Files rule also instructs *tripwire* to watch the policy configuration and key files. Note that in the file severity section earlier, SEC\_BIN was defined to be ReadOnly, so you're telling *tripwire* that the policy, configuration, and key files should not change at all. Here's an example of the Tripwire Date Files rule:

```
```
# Tripwire Data Files - Configuration Files, Policy Files, Keys, Reports, Databases

(rulename = "Tripwire Data Files", severity = $(SIG_HI))
{
  $(TWDB)    -> $(Dynamic) -i;
  $(TWPOL)/tw.pol    -> $(SEC_BIN) -i;
  $(TWBIN)/tw.cfg    -> $(SEC_BIN) -i;
```
```