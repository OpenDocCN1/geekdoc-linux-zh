# Penetration Testing with Kali Linux

The output shows that this contains dave's password in plaintext. Wow! This is a potential gold mine of information. In a real-world situation, we would need to perform significantly more information gathering (including the actual username associated with each password), but for purposes of demonstration we will run with this!

Let's try to use the private key id_rsa for the newly-identified user in an SSH connection. For this, we must modify the permissions of the downloaded private key. The SSH port used in this example is 2222. We try each of these passphrases as the passphrase for the SSH private key. Note that the ssh password will not echo the passphrase.

```
kali@kali:~/passwordattacks chmod 600 id_rsa

kali@kali:~/passwordattacks ssh -i id_rsa -p 2222 dave@192.168.50.201
The authentication of "192.168.50.201:2222" can't be established.
ED25519 key fingerprint is SHA256:ac7a8Mzb+0f5xv1tdQsw/5nn33/0GAIRuonao4.
This key is not known by any other hosts
Are you sure you want to continue (yes/no/fingerprint)?? yes
Warning: Permanently added 192.168.50.201:2222 (ED25519) to the list of known hosts.
```

Enter passphrase for key 'id_rsa':
Enter passphrase for key 'id_rsa':
Enter passphrase for key 'id_rsa':
dave@192.168.50.201's password: 

```
kali@kali:~/passwordattacks ssh -i id_rsa -p 2222 dave@192.168.50.201
Enter passphrase for key 'id_rsa':
Enter passphrase for key 'id_rsa':
Enter passphrase for key 'id_rsa':
```

Listing 280 - SSH connection attempts with the private key

None of the passwords from the text file worked for this passphrase. However, in a real penetration test we would keep these passwords on for various vectors including spray attacks, attacks against a dave on other systems. However, we still need a passphrase for dave's private key.

According to the note.txt, a new password policy was enacted in January 2022. There's a high probability that dave has a cracking methodology that satisfies the new password policy.

Following the cracking methodology, our next step is to transform the private key into a hash format for our cracking tools. We will use the ssh2john transform script from the JIT suite and save the result to ssh.hash

```
kali@kali:~/passwordattacks ssh2john id_rsa > ssh.hash

kali@kali:~/passwordattacks cat ssh.hash
id_rsa=$ssh$6$16750598e7a83d3764eae183fcdf592feb7b18945f67056f736782d6b65792d6b65792d76310
0000000a165733235362d63472000000006263271972797740000018000001107592e7a83d3764eae883
fcdf592feb7000010000000000...
```

Listing 281 - Using ssh2john to format the hash

PWK - © 2023 OffSec Services Limited. All rights reserved.

405