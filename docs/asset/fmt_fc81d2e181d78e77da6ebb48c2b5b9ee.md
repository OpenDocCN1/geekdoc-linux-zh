
# 65: 01000000 /3 包含 64-69 需要列出

```
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 65.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 66.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 67.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 68.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 69.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 70.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 71.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 72.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 73.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 74.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 75.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 76.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 77.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 78.0.0.0/8 -0
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 79.0.0.0/8 -0
```

# 80: 01000000 /4 掩码 80-95

```
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 80.0.0.0/4 -0
```

# 96: 01100000 /4 掩码 96-111

```
ipfwadm -a deny -W EXTERNAL_INTERFACE -S 96.0.0.0/4
```
