page 568 for further information on the DNLC operation.) The number of entries in the DNLC is set by the system-tunable parameter, `ncsize`, which is set at boot time by the calculations shown in Table 15-2. The `ncsize` parameter is calculated in proportion to the `maxusers` parameter, which is equal to the number of megabytes of memory installed in the system, capped by a maximum of 1024. The `maxusers` parameter can also be overridden in `/etc/system` to a maximum of 2048.

# Table 15-2 DNLC Default Sizes

| Solaris Version | Default ncsize Calculation |
|---|---|
| Solaris 2.4, 2.5, 2.5.1 | `ncsize = (17 × maxusers) + 90` |
| Solaris 2.6, 2.7 | `ncsize = (68 × maxusers) + 360` |

The size of the DNLC rarely needs to be adjusted because the size scales with the amount of memory installed in the system. Earlier Solaris versions had a default maximum of 17498 (34906 with maxusers set to 2048), and later Solaris versions have a maximum of 69992 (139624 with maxusers set to 2048).

Use adb to determine the size of the DNLC.

```
```text
# adb -k
physmem b919
ncsize/D
ncsize:		25520
```
```

The hit rate of the directory name cache shows the number of times a name was looked up and found in the name cache. A high hit rate (>90%) shows that the DNLC is working well. A low hit rate does not necessarily mean that the DNLC is undersized; it simply means that we are not always finding the names we want in the name cache. This situation can occur if we are creating a large number of files.