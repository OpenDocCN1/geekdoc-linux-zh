```
nmap -p 80,443 target_ip
```

Scans only specified ports (80 and 443 in this example).

# 9. Scan All 65535 Ports:

```
nmap -p- target_ip
```

Scans all 65535 ports. This can take longer but ensures no port is overlooked.

# 10. Output to a File:

```
nmap -oN output.txt target_ip
```

Saves the results to a file named "output.txt" in normal format.

# 11. Output in XML Format:

```
nmap -oX output.xml target_ip
```

Saves the results in XML format.