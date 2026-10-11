OPTIONS:
  -h Show this help information
  -o <file> Send output to a file in csv format
  -S <string> Search string for row filter

+   Keywords:
+     aka : Modules with a matching AKA (also-known-as) name
+     author : Modules written by this author
+     arch : Modules affecting this architecture
+     bid : Modules with a matching Bugtraq ID
+     cve : Modules with a matching CVE ID
+     ...
+     target : Modules affecting this target
+     type : Modules of a specific type (exploit, payload, auxiliary, encoder, eva

Examples:
  search cve:2009 type:exploit

```
msf5 > search type:auxiliary name:smb
```

Matching Modules
==============

| Name | Rank | Description |
|---|---|---|
| auxiliary/admin/oracle/ora_ntlm_stealer | normal | Oracle SMB Relay Code Execution |
| auxiliary/admin/smb/check_dir_file | normal | SMB Scanner Check File/Directory |
| auxiliary/admin/smb/delete_file | normal | SMB File Delete Utility |
| auxiliary/admin/smb/download_file | normal | SMB File Download Utility |

Listing 746- Searching for SMB auxiliary modules

After invoking a module with use, we can request more info about it as follows:

```
msf5 > use scanner/smb/smb2

msf5 auxiliary(scanner/smb/smb2) > info
```

Name: SMB 2.0 Protocol Detection
Module: auxiliary/scanner/smb/smb2
License: Metasploit Framework License (BSD)
Rank: Normal

Provided by:
  hdm <x@hdm.io>

Check supported:
  Yes

| Name | Current Setting | Required | Description |
|---|---|---|---|
| RHOSTS |  | yes | The target address range or CIDR identifier |
| RPORT | 445 | yes | The target port (TCP) |
| THREADS | 1 | yes | The number of concurrent threads |