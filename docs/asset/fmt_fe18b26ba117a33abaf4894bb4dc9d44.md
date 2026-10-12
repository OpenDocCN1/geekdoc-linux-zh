
# `<device>` 和 `<nametoaddr_libs>` 字段在此实现中始终是空的：

```
udp tpi_clts v inet udp
tcp tpi_cts_ord v inet tcp
udp6 tpi_clts v inet6 udp
tcp6 tpi_cts_ord v inet6 tcp
rawip tpi_raw - inet
local tpi_cts_ord loopback
unix tpi_cts_ords loopback
```
