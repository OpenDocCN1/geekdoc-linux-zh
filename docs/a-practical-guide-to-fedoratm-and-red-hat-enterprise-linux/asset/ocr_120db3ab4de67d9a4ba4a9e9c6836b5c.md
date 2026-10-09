authentication key on the client (local system), place the public part of the key on the server, and keep the private part of the key on the client. When you connect to the server, it issues a challenge based on the public part of the key. OpenSSH then uses the private part of the key to respond to this challenge. If the client provides the appropriate response, the server logs you in.

The first step in setting up an automatic login is to generate your personal authentication keys. First check whether these authentication keys already exist on the local system (client) by looking in `~/.ssh` for either `id_dsa` and `id_dsa.pub` or `id_rsa` and `id_rsa.pub`. If one of these pairs of files is present, skip the next step (do not create a new key).

![](bbox=[0.07, 0.28, 0.21, 0.32])

On the client, the `ssh-keygen` utility creates the public and private parts of an RSA key. The key’s randomart image is a visual representation of the public key; see page 702.

```
$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/sam/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/sam/.ssh/id_rsa.
Your public key has been saved in /home/sam/.ssh/id_rsa.pub.
The key fingerprint is:
23:8f:99:2e:43:36:93:ed:c6:38:fe:4d:04:61:27:28 sam@guava
The key’s randomart image is:
+-- ( RSA 2048 )----+
|    + .             |
|  E. ..+            |
|    . . . .         |
| o.  S              |
| * .B .             |
|  O  o+ o           |
|    =.,+o           |
|    .,.+O           |
|                     |
+--------

```

Replace `rsa` with `dsa` to generate DSA keys. In this example, the user pressed RETURN in response to each query. You have the option of specifying a passphrase (10–30 characters is a good length) to encrypt the private part of the key. There is no way to recover a lost passphrase. See the security tip on page 703 for more information about the passphrase.

![](bbox=[0.07, 0.77, 0.21, 0.82])

The `ssh-keygen` utility generates two keys: a private key or identification in `~/.ssh/id_rsa` and a public key in `~/.ssh/id_rsa.pub`. No one except the owner should be able to write to either of these files, and only the owner should be able to read from the private key file.

You can display the local server’s RSA key fingerprint using `ssh-keygen:`

```
$ ssh-keygen -lF /etc/ssh/ssh_host_rsa_key.pub
2048 d1:9d:1b:5b:97:5c:80:ed:4b:4d:9a:b7:bc:1a:ea:a1 /etc/ssh/ssh_host_rsa_key.pub (RSA)

```

Or you can display the fingerprint of the public key you just created:

```
$ ssh-keygen -lF ~/.ssh/id_rsa.pub
2048 23:8f:99:2e:43:36:93:ed:c6:38:fe:4d:04:61:27:28 /home/sam/.ssh/id_rsa.pub sam@plum (RSA)

```