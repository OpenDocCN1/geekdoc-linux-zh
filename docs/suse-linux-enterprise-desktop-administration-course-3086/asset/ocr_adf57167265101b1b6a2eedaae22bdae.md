+   2. Using the password `pN0v3ll`, check the processes running on your partner’s system by entering
+   
+      `ssh -l root partner_IP_address ps aux`
+   
+      A list of all processes currently running on your partner’s computer is displayed.
+   
+   3. Using the password `novell`, copy your partner’s `/etc/hosts` file to your `/tmp` directory by entering
+   
+      `scp geeko@partner_IP_address:/etc/hosts /tmp/`
+   
+   4. Using the password `novell`, copy your `/etc/hosts` file to geeko’s directory on your partner’s computer by entering
+   
+      `scp /etc/hosts geeko@partner_IP_address:`
+   
+   5. Use sftp to connect to your partner’s computer as geeko by entering
+   
+      `sftp geeko@partner_IP_address`
+   
+   6. Copy the `/bin/date` program to geeko’s directory on your own computer by entering
+   
+      `get /bin/date /home/geeko/`
+   
+   7. Quit sftp by entering
+   
+      `exit`

# Public Key Authentication Management

Besides password authentication, a user can also authenticate using a public key procedure. Protocol version 1 only supports RSA keys. Protocol version 2 provides authentication through RSA and DSA keys.

To manage public key authentication, you need to know the following:

+   - Public Key Authentication Process
+   - Create a Key Pair
+   - Configure and Use Public Key Authentication

# *Public Key Authentication Process*

To use public key authentication, the public key of the user has to be stored on the server in the home directory of the user account being accessed. These public keys are stored on the server in the file `~/.ssh/authorized_keys`. The corresponding private key must be stored on the client computer.

With the keys stored in the appropriate places, the following occurs in the public key authentication process:

+   1. The client informs the server which public key is being used for authentication.
+   2. The server checks to see if the public key is known.
+   3. The server encrypts a random number using the public key and transfers this to the client.
+   4. Only the client is able to decrypt the random number with its private key.
+   5. The client sends the server an MD5 checksum that it has calculated from the number.