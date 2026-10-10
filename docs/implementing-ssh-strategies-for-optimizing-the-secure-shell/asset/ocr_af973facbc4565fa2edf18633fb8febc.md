# *Network Settings*

The network section of the sshd2\_config file should look like the following:

```
    Port                        443
    ListenAddress               0.0.0.0
    RequireReverseMapping        no
    ResolveClientHostName        yes
    MaxBroadcastsPerSecond       0
    NoDelay                      yes
    KeepAlive                    yes
```

The network section of the SSH configuration GUI should look like Figure 2.3.

![](bbox=[0.14, 0.34, 0.64, 0.6])

**Figure 2.3**  Network screen from the SSH server configuration tool.