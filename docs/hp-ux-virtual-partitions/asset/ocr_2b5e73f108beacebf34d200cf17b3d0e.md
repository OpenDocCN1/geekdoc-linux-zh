# Virtual Partition Command Summary

| Command | Description |
| :--- | :--- |
| `ISL>` | Virtual Partition Monitor is loaded from `ISL` with: `ISL> hpxuc /stand/vpmon` |
| Initial System Load prompt `MON>` | To load Virtual Partitions directly from `ISL>`, use: `ISL> hpxuc /stand/vpmon vparload -p vPar_name` |
| `MON>` | This is loaded from `ISL` with: `ISL> hpxuc /stand/vpmon` |
| Virtual Partitions Monitor prompt (also see `vparload` command.) | To load an alternate database from `ISL`, use: `ISL> hpxuc /stand/vpmon -D db_file`<br>To load one vPar from `MON` use:<br>`MON> vparload vPar_name`<br><br>Many other commands can be issued from `MON`. Type `help` or `?` to list.<br>(Commands include: `scan`, `vparinfo`, `ls`, `log`, `getauto`, `lifls`, `cbuf`, `cat`). |
| `vparload`<br>Load Virtual Partitions from `MON>` prompt only. | form1: `vparload -all`<br>form2: `vparload -auto`<br>form3: `vparload -p vp_name [-b kernelpath] [-o "boot_options"] [-B hardware_path]`<br><br>To boot a Virtual Partition from `MON>`:<br>`MON> vparload -p vPar_name`<br><br>To boot all Virtual Partitions from `MON>`:<br>`MON> vparload -all`<br><br>To boot a Virtual Partition in single-user mode from `MON>`:<br>`MON> vparload -p vPar_name -o "-1s"`<br><br>Some other options to issue at `MON>` include:<br>`-1q` (low quorum), `-1m` (maintenance mode) |
| `vparboot`<br>Boot a Virtual Partition from the command line only. | form1: `vparboot -p vp_name [-b kernel_path] [-o boot_opts]`<br>          `[-B boot_addr]`<br>form2: `vparboot -p vp_name -1ignite_kernel`<br><br>To boot a Virtual Partition from the command line:<br>`# vparboot -p vPar_name`<br><br>To boot a Virtual Partition from the command line in single-user mode:<br>`# vparboot -p vPar_name -o "-1s"` |