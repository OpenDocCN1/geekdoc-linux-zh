As a general rule, you don't tend to work directly with gated at this point. One of this daemon's companion programs is gdc, which is the gated controller. Even if you've already installed gated, you might not have gdc. It seems that some distributions don't include gdc as part of the gated package, nor even in a separate one. However, gdc does come with the main gated public source, which you can get by going to www.gated.org.

# Starting gdc

The gdc program itself doesn't run continuously. Each time you want to use it, you have to use the necessary flags and commands. The flags are listed in Table 5.25. As soon as you have gdc and its flags typed in, add the commands specified in the following section. This allows you to manipulate gated without having to actually touch the daemon itself. Doing this can save a lot of angst and heartache down the road.

| Table 5.25 Command-Line Switches Available When Starting gdc |
| Flag | Purpose | Format | Value(s) |
| -c | Sets the maximum allowed size of a gated coredump—only when gated is started using gdc. | -c size | Size in bytes. |
| -f | Sets the maximum allowed size of a gated state dump file—only when gated is started using gdc. | -f size | Size in bytes. |
| -m | Sets the maximum allowed data segment size for gated—only when gated is started using gdc. | -m size | Size in bytes. |
| -n | Sets gated to not alter the kernel forwarding table. | -n | N/A |
| -q | Sets gated to run in quiet mode, sending nothing to STDOUT. Error messages are logged according to settings in syslog.conf. | -q | N/A |