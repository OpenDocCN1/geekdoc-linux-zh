```
publisher: Colin King (cking-kernel-tools)
store-url: https://snapcraft.io/stress-ng
contact:    colin.king@canonical.com
license:    GPL-2.0
description: |
    stress-ng can stress various subsystems of a computer. It can stress load
    CPU, cache, disk, memory, socket and pipe I/O, scheduling and much more.
    stress-ng is a re-write of the original stress tool by Amos Waterland but
    has many additional features such as specifying the number of bogo
    operations to run, execution metrics, a stress verification on memory and
    compute operations and considerably more stress mechanisms.
snap-id: YMJsyw4vySPDs8BcA7jx8U0tOVShUt6
channels:
  latest/stable:    V0.11.24    2020-11-13 (5273) 3MB -
  latest/candidate: V0.11.24    2020-11-13 (5273) 3MB -
  latest/beta:      V0.11.24    2020-11-13 (5273) 3MB -
  latest/edge:      V0.11.24-44-20201121-7613-g2627a 2020-11-21 (5298) 3MB -
$ 
```

To install a new snap, use the snap install command.

$ sudo snap install stress-ng

[sudo] password for rich:

stress-ng V0.11.24 from Colin King (cking-kernel-tools) installed
$ 

You can check that the software container was installed by using the list command:

$ snap list

| Name | Version | Rev | Tracking | Publisher | Notes |
|------|---------|-----|----------|-----------|-------|
| core18 | 20200929 | 1932 | latest/stable | canonical\* | base |
| lxd | 4.0.4 | 18150 | 4.0/stable/... | canonical\* | - |
| snapd | 2.47.1 | 9721 | latest/stable | canonical\* | snapd |
| stress-ng | V0.11.24 | 5273 | latest/stable | cking-kernel-tools | - |
$ 

Finally, you can remove an installed application container by using the remove command:

$ sudo snap remove stress-ng

stress-ng removed
$ 

As the snap is removed, you’ll see some messages about the progress of the removal. Instead of removing a snap, if you prefer you can just disable it without removing it. Just use the snap disable command. To reenable the snap, use the snap enable command.