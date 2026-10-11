
gateway machine will encrypt all the information passing through the untrusted network. The machine also decrypts the information at the destination. The IPSEC gateway machine led to the development and use of Virtual Private Networks or VPNs to ensure there is a secure network used by machines, especially if they are connected to the same server or network from different locations and devices.

### Secure Telnet (stelnet) and Secure Shell (ssh)

ssh and stelnet are a collection or suite of programs that enable a user to log in to the server or system remotely. These programs use an encrypted connection which allows them to log in safely.

Another suite of programs called openssl is used as a replacement for rcp, login, and rsh. This is a secure alternative to these programs. This suite encrypts the communication or data passed between hosts through public-key cryptography. It also can be used to authenticate users on the server or system. This program can also be used by users to log in to the server remotely. Once they are logged in, users can copy the data between hosts and prevent DNS spoofing, man-in-the-middle, and other hacks. The suite compresses the data passed between users and secures the data passed between the connection.

SSLey is another SSL protocol that has many features like stelnet. It was developed as part of Netscape’s SSL protocol. It can be used on numerous databases and algorithms, including IDEA, DES, and Blowfish.

### Pluggable Authentication Modules or PAM

New versions of Red Hat Linux and Debian Linux distributions use a unified authentication mechanism to move data between networks and other logical connections. This is termed as PAM or Pluggable Authentication Modules. These modules allow users to change their authentication methods and requirements as and when they need to. They can also use these modules to encapsulate any local authentication methods used without having to recompile the information or binaries. The following are functions you can perform using PAM:

- Prevent Denial of Service (DoS) attacks from users by setting resource limits for each user
- Allow users to log in to the server only from specific devices and places at specific time intervals
- Use shadow passwords (we will cover this shortly)
- Use different forms of encryption, including DES, for passwords to ensure they cannot be detected through brute-force attacks

If you have this enabled in your server or network, you can prevent numerous attacks before they occur on your system.

## CIPE or Cryptographic IP Encapsulation

The objective of this encryption is to provide a facility that is secure for the server and system. This encryption protects the interconnection between subnetworks across insecure packet networks from traffic analysis, eavesdropping, and faked message injection. Using CIPE, you can encrypt the data at both the server and network levels. All the information moving along the network in the form of packets is encrypted, and these packets are received and sent by an encryption engine that is next to the network driver.

CIPE does not encrypt the data that is passed through the network or connection. It does not even encrypt the data at the network or socket levels. It will only encrypt the logical connection between networks, sockets, and programs found on different hosts. This is very different from SSH. You can also use CIPE to create new VPNs through tunneling. If you want to avoid making changes to the application software being used, you can use low-level encryption methods. These methods ensure the logical connection between two networks connected in the VPN or Virtual Private Network work transparently.

## Using Shadow Passwords

You can use shadow passwords to ensure a user’s password is encrypted and the information is maintained in a file that normal users cannot access. New versions of RedHat and Debian Linux use this setting as a default. After encryption, the passwords are stored in a file in the server directory that every user on the server can access. If one were to run a password cracking or guesser program on the file, they could obtain every user's password on the system.

A shadow password will be stored in a different file which can be accessed only by an administrator or privileged users. If you want to use shadow passwords, you need to ensure that every application, tool or utility which needs the password can access the information. You may also need to recompile the list of passwords to support the user’s access to the system. Using PAM, you can plug in a shadow module that does not require you to recompile any of the system's passwords.

## John the Ripper and Crack

If you use a password program on your server, but you notice that hard-to-guess passwords are not used, then you need to run a password cracking program. This program will help you determine if the passwords used by you and your users are safe and secure. The idea behind a password cracking program is simple – the program will look at every word in the dictionary and try variations of the same words. It will also encrypt the words and check those words against your password. If the program finds a match, it will know the user's password.

There are numerous password-cracking programs you can use, but people often use “John the Ripper” and “Crack.” These programs may take up your CPU's time but give excellent results. Before a hacker uses these programs on your system and server, you need to use them and check if there are any weak passwords. If yes, ask the users to change them immediately to avoid any hacks. You may wonder how the hacker can access the password file on the server when he can only access the server through a hole or vulnerability. Unfortunately, there are holes in the server, and an experienced hacker can find those holes easily.

You can also try other encryption methods used in Linux, such as Transparent Cryptographic File System (TCFS), Cryptographic File system, display security, X11, and SVGA. We will look at them in detail later in the book.

# Chapter Six

# Tools to Encrypt and Decrypt Password Protected Files

The process of encoding or protecting files to ensure only selected users can access the file is termed encryption. We have been using the concept of encryption even before computers came into existence. When countries were at war, they developed codes to communicate with their spies or soldiers in the warzone. This was one way for them to ensure nobody else could understand the message that was being passed.

Linux distributions come with standard tools used to encrypt and decrypt the information in the system or server. In this chapter, we will look at seven tools you can use to encrypt and decrypt files using a password.

## GNU Privacy Guard or GnuPG

GnuPG, often called GPG, is a collection or suite of various cryptographic software and is written in C language. If you want to use this to encrypt and decrypt files, it is best to download the file’s latest version. Most Linux distributions released in the last few years will come with this package installed as a default. If you find that it is not installed in your server or system, use the following commands to install it:

```bash
$ sudo apt-get install gnupg
# yum install gnupg
```

Across all the examples in this chapter, we will use a file called tecmint.txt file to encrypt and decrypt. This file is on the desktop of the system and will be moved to a different location if required. Before we go ahead, let us look at the content in this file. To do this, run the following command: `$ cat ~/Desktop/tecmint/tecmint.txt`.

You can now encrypt the tecmint.txt using the tool. When you run the GPC command using the ‘-c’ option. This is a symmetric cipher, and it will create the encrypted file with the extension ‘.gpg’ against the file tecmint.txt. You can look at the content in the directory to determine which file was encrypted:

```bash
$ gpg -c - ~/Desktop/Tecmint/tecmint.txt
$ ls -l ~/Desktop/Tecmint
```

You need to enter the word ‘paraphrase’ twice if you want to encrypt any file. In the above example, we have used the encryption algorithm CA S T5 to encrypt the file. You can specify a different algorithm if you use a specific one often. If you want to look at the different algorithms available to you, enter the following command: $ gpg −version.

To decrypt the file we have encrypted above, you need to use the commands below. Before you do this, you need to remove the original file from the desktop and only leave the encrypted file. We do this since the decryption algorithm will replace the encrypted file with the original file, and you may receive an error if you have the older file on the desktop while you perform the decryption. The commands to run are:

```bash
$ rm ~/Desktop/Tecmint/tecmint.txt
$ gpg ~/Desktop/Tecmint/tecmint.txt.gpg
```

It is important for you to remember the password you use at the time of encryption. You need to use the same password if you want to decrypt the file.

## Bcrypt

Bcrypt is a function based on the Blowfish cipher, and the developers tried to ensure that the algorithm used was not as weak as the Blowfish cipher. Most organizations stopped using the Blowfish cipher when they learned that users could attack the algorithm from anywhere because of a small vulnerability. To install the tool on your system, run the following commands:

```bash
$ sudo apt-get install bcrypt
# yum install bcrypt
```

When you encrypt the file, you need to run the following command: $ bcrypt ~/Desktop/Tecmint/tecmint.txt. When you run this command, the server will create a new file on your desktop and replace the original file. To decrypt the file, you need to run the command: $ bcrypt tecmint.txt.bfe.
