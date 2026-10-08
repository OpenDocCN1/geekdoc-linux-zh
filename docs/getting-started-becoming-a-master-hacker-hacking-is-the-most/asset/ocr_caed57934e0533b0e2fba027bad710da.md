kali > cd /etc kali > cat shadow This file includes all the accounts on your system and their password hashes. Since I only have one password on the root account, only one hash appears. The password hash appears after the username “root:” and before the next colon “:”. It is this indecipherable set of characters that represent the password that we need to crack.

On Windows systems, the password hashes for the local user are stored at: C:\Windows\System32\config\SAM



![](bbox=[0.12, 0.4, 0.88, 0.7])