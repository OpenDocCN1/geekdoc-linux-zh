By default, sshd uses a secure challenge-response authentication method that ensures that the password is not transmitted on the network, but this can be changed to Kerberos authentication or authentication that allows users based on the ~/.rhosts or /etc/hosts.equiv files.

Organizations use many types of encryption to secure communication on the network. Each type of encryption differs in its method of encryption and the cryptography key length used to encrypt data; the longer the key length, the more difficult it is for malicious users to decode the data. The main types of encryption supported by sshd are as follows:

+   - Triple Data Encryption Standard (3DES), which encrypts blocks of data in three stages using a 168-bit key length
+   - Advanced Encryption Standard (AES), which is an improvement on 3DES encryption and is available in 128-, 192-, and 256-bit key lengths
+   - Blowfish, which is an encryption algorithm that is much faster than 3DES and can use keys up to 448 bits in length
+   - Carlisle Adams Stafford Tavares (CAST), which is a general-purpose encryption similar to 3DES and is commonly available using a 128-bit key length
+   - ARCFour, which is a fast encryption algorithm that operates on streams of data instead of blocks of data and uses variable-length keys up to 2048 bits in length

In addition, all of the aforementioned types of encryption except ARCFour typically use Cipher Block Chaining (CBC), which can be used to encrypt larger amounts of data.

![](bbox=[0.11, 0.56, 0.91, 0.58])

> Client computers can use a /etc/ssh/ssh_config or $HOME/ssh/ssh_config file to set ssh options for use with their ssh client utility. The authentication and encryption settings on the client computer must match those in the server configuration file (/etc/ssh/sshd_config) for a connection to be successful.

# # Routing and Firewall Services

Some network services are not provided entirely by network daemons; instead, these services are provided by the Linux kernel and do not listen to a particular port. The two most common of these types of services are routing and firewall services.

# ## Routing

Every computer on a network maintains a list of TCP/IP networks so that packets are sent to the appropriate location; this list is called a **route table** and is stored in system memory. To see the route table, you can simply use the **route command**, as shown in the following output: