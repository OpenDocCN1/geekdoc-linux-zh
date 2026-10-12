With the **arp** command, the superuser can:

+   - display the ARP cache
+   - delete an ARP entry
+   - add an ARP entry

The ARP tool provides a number of command-line options. However, only the most important ones are listed in Table 4.1 and fully described below. Each of these options supports either a single command character or keyword, along with two dashes at the beginning. For instance, the **-v** option has an associated **--verbose** keyword. These are equivalent and can be used interchangeably on the command line. Table 4.1 shows both forms. The reason to choose one over the other is merely a matter of style. However, the keyword format may make it easier to remember individual options in the future.

# **Displaying the ARP Cache**

**Table 4.1** *Important arp command-line options*

| Option | Keyword | Description |
| :--- | :--- | :--- |
| -a | --display | Displays the current ARP entry for a specific host |
| -d | --delete | Deletes an ARP entry |
| -f | --file | Loads a file that contains entries to place in the cache |
| -i | --device | Displays only those entries for specified interface |
| -n | --numeric | Shows numerical addresses instead of hostnames |
| -s | --set | Creates an ARP entry |
| -v | --verbose | Displays ARP cache using verbose mode |

To display the contents of the ARP table, use the **arp-v (–verbose)** command. When the table is displayed, it includes the device name, hardware type, physical address, mask flag, and network interface. A sample is shown: