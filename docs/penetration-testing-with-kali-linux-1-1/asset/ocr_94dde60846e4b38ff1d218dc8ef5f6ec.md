Although this required some investigation of the application, the result is worth it as a valid password was discovered. The other service modules included with Hydra are well worth the effort to master.

# 19.3.4.1 *Exercises*

(Reporting is not required for these exercises)

+   Run the HTTP POST password attack against the web form on your Windows client.
+   Perform a FTP password attack against the Pure-FTPD application on your local Kali Linux machine.

# ## 19.4 Leveraging Password Hashes

Next, we turn our attention to attacks focused on the use of *password hashes*.

A cryptographic *hash function*562 is a one-way function implementing an algorithm that, given an arbitrary block of data, returns a fixed-size bit string called a “hash value” or “message digest”. One of the most important uses of cryptographic hash functions are their application in password verification.

# 19.4.1      *Retrieving Password Hashes*

Most systems that use a password authentication mechanism need to store these passwords locally on the machine. Rather than storing passwords in clear text, modern authentication mechanisms usually store them as hashes to improve security. This is true for operating systems, network hardware, and more. This means that during the authentication process, the password presented by the user is hashed and compared with the previously stored message digest.

Identifying the exact type of hash without having further information about the program or mechanism that generated it can be very challenging and sometimes even impossible. The *Openwall website*563 can help identify the source of various password hashes. When attempting to identify a message digest type, there are three important hash properties to consider. These include the length of the hash, the character set used in the hash, and any special characters used in the hash.

A useful tool that can assist with hash type identification is **hashid**564. To use it, we simply run the tool and paste in the hash we wish to identify:

```
```
kali@kali:~$ hashid c43ee559d69bc7f691fe2fbfe8a5ef0a
Analyzing 'c43ee559d69bc7f691fe2fbfe8a5ef0a'
[+] MD2
[+] MD5
[+] MD4
[+] Double MD5
[+] LM
```
```

562  (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cryptographic_hash_function
563  (Openwall, 2019), http://openwall.info/wiki/john/sample-hashes
564  (Pspanda, 2015), https://pspanda.github.io/hashID/