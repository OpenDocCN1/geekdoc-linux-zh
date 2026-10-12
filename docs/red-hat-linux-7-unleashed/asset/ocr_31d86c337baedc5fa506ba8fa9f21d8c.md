Each keyword is the name to one of the /etc files that can be controlled by /etc/nsswitch.conf. The keywords that can be included follow:

| Keyword (Filename) | Function |
| :--- | :--- |
| aliases | Mail aliases |
| passwd | System users |
| group | User groups |
| shadow | Shadow passwords |
| hosts | Hostnames and IP addresses |
| networks | Network names and numbers |
| protocols | Network protocols |
| services | Port numbers and service names |
| ethers | Ethernet numbers |
| rpc | Remote Procedure Call names and numbers |
| netgroup | Networkwide groups |

The methods that can be included follow:

| Method | Meaning |
| :--- | :--- |
| files | Valid for all keywords except netgroup. Look for record in the corresponding /etc file. |
| db | Valid for all keywords except netgroup. Look record up in the corresponding database in the /var/db directory. This is useful for extremely long files, such as passwd files with more than 500 entries. To create these files from the standard /etc files, cd into /var/db and run the make command. |
| compat | Compatibility mode, valid for passwd, group, and shadow files. In this mode, lookups are made first to the corresponding /etc file. If you want to do NIS lookup of the corresponding NIS database, you need to include a line where the first field (username or groupname) is a plus character, followed by an appropriate number of colons (six for /etc/passwd, three for /etc/group, eight for /etc/shadow). For example, in /etc/passwd, the following line would have to be included at the end: |