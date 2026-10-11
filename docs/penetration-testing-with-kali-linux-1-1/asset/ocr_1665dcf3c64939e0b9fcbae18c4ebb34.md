| Variable_name | Value |
|---|---|
| alter_algorithm | DEFAULT |
| aria_block_size | 8192 |
| aria_checkpoint_interval | 30 |
| ... | |
| **hostname** | **zora** |
| identity | 0 |
| ... | |
| pid_file | /run/mysql/mariadb.pid |
| **plugin_dir** | **/home/dev/plugin/** |
| plugin_maturity | gamma |
| port | 3306 |
| preload_buffer_size | 32768 |
| profiling | OFF |
| ... | |
| tmp_memory_table_size | 16777216 |
| tmp_table_size | 16777216 |
| **tmpdir** | **/var/tmp** |
| transaction_alloc_block_size | 8192 |
| ... | |
| userstat | OFF |
| **version** | **10.3.28-MariaDB** |
| version_comment | MariaDB Server |
| **version_compile_machine** | **x86_64** |
| version_compile_os | Linux |
| version_malloc_library | system |
| ... | |
| wsrep_sst_receive_address | AUTO |
| wsrep_start_position | 00000000-0000-0000-0000-000000000000: |
| wsrep_sync_wait | 0 |
| 639 rows in set (0.154 sec) |

*Listing 93 - Showing all variables*

From this one query we learned a few things. First, we found that the hostname is “zora”. From this point on, we will refer to the MariaDB host as Zora. Next, we also learned that the **tmp** directory is in **/var/tmp**. We also confirm again that we are running MariaDB version 10.3.20 but we now also learn that the target architecture is **x86_64**. The most interesting piece of information we can gather is that the **plugin_dir** is set to **/home/dev/plugin/**. This directory is not standard for MariaDB. Let’s take note of that as it might become useful later on.

Now that we have gathered some information, let’s see if we can find any exploits for our target MariaDB version.

```
kali@kali:--$ searchsploit mariadb
```

| Exploit Title | Path (\usr/share/exploitdb/) |
|---|---|
| MariaDB Client 10.1.26 - Denial of Service (PoC) | exploits/linux/dos/45901.txt |
| MySQL / MariaDB - Geometry Querry Denial of Service | exploits/linux/dos/38392.txt |
| MySQL / MariaDB / PerconaDB 5.5.51/5.6.32/5.7.14 - Co | exploits/linux/local/40360.txt |
| MySQL / MariaDB / PerconaDB 5.5.x/5.6.x/5.7.x - 'mysq | exploits/linux/local/40678.c |
| MySQL / MariaDB / PerconaDB 5.5.x/5.6.x/5.7.x - 'root | exploits/linux/local/40679.sh |
| Oracle MySQL / MariaDB - Insecure Salt Generation Sec | exploits/linux/remote/38109.pl |