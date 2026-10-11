
## Using Encryption

In this chapter, you will learn about:
- How encryption works
- Encrypting remote access with OpenSSH
- Encrypting Linux files

As mentioned at the beginning of the preceding chapter, information security is a key issue in nearly every organization. If it isn't, it should be. Twenty years ago, we in the IT industry just didn't worry all that much about information security. That's because society in general didn't worry all that much about information security. Let me give you two examples.

First, when I was an undergraduate in the late 1980s and early 1990s, it was common for my professors to post exam scores in the hallway outside their office using students' Social Security numbers. I chuckle when I recall the reason why; it was to protect students' privacy. Heaven forbid you would associate a name with a test score, let's just use their SSNs!

State and federal governments were not immune to this type of practice either. Again, when I was in college, my home state used your Social Security number as your driver's license number. They printed it right on the license itself. Therefore, every time you used your driver's license for ID, you were revealing your SSN. What's worse, we used checks a lot more back then than we do now. Guess what every store clerk wrote on each check? Yep, they recorded your driver's license number. That means each check I wrote in college had my SSN and my bank account number recorded on it. Sheesh!

Today, we think doing something like this would be crazy. Back then, we didn't think anything of it. That has all changed in today's security-conscious world. Folks who wear black hats have figured out that a minimal amount of information can yield huge profits, and they will stop at nothing to get it. As a result, we who wear white hats have to be almost obsessive about information security.

Information security is focused on protecting the valuable electronic information of organizations and users. Thus, the demand for IT professionals who know how to secure networks and computers is at an all-time high. As a Linux system administrator, you need to be very aware of the security issues affecting your implementation. In the preceding chapter, we spent some time looking at several policies and practices you can put in place to help secure your systems. In this chapter, we're going to expand on what you learned in the last chapter and discuss how you can use encryption to increase the security of your Linux systems and network.

> **TIP** Information security is a huge topic that we can’t adequately address in this book. I highly recommend that you enhance your knowledge by getting your Security+ certification from CompTIA. The IT world has become the modern equivalent of the Wild West from American history. You need to know how to thoroughly protect your data from malicious black hats!

### How Encryption Works

Let’s begin by discussing how encryption works.

Hearken back with me, if you will, to your elementary school days. Did you ever pass notes to your friends? I know that in the modern era of mobile devices and text messaging this may seem archaic; but when I was a kid, notes were a vital means of communication at school. After all, you had important business to conduct, right?

If your school was like mine, these extracurricular forms of communication were strictly forbidden in class. If a teacher intercepted a poorly handled note pass, you could be sure it would be read in front of the class, which could be a fate worse than death (especially if the note contained information about who currently likes whom).

To prevent this, my buddies and I developed codes to encrypt our notes. If one of them was intercepted, we could rest assured that the teacher wouldn’t be able to read it to the rest of the class. As fourth graders, our encoding mechanisms were primitive. For the most part, we used two codes. The first one involved skewing the alphabet down a letter or two, as shown here:

```
ZABCDEFGHIJKLMNOPQRSTUVWXYZ
ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

> **NOTE** This simple encryption technique is called a *letter shift*.

We would use the bottom line for the clear text and the top line for the cipher text. For example, the clear text “JAKE LIKES PAM” would come out “LIZD KHJFR OZL” when encoded. Eventually, our teacher started getting wise to this code and figured out how to crack it. Therefore, we switched to a different code using numbers and letters, as shown here:

```
 2  6  1  2  3  4  5  6  7  8  9 10 11....
A  B  C  D  E  F  G  H  I  J  K  L ...
```

Using this code, my friend Jake’s name would be encoded as 9 26 10 4. This basic concept of using keys to scramble and descramble messages can be used to encode network communications as well. In today’s security-conscious world, the need to encrypt the contents of network communications is preeminent. Using network monitoring tools (such as nmap discussed in the preceding chapter), it is relatively easy for a mischievous individual to sniff out network transmissions and read them. If they contained sensitive information, such as usernames, passwords, financial data, credit card numbers, or personal information, we could have a real problem on our hands.

To protect this information, we need to encrypt critical network communications. Unlike the simple codes I used in the fourth grade, network cryptography today uses much more sophisticated encoding mechanisms. There are two general approaches to doing this:
- Symmetric encryption
- Asymmetric encryption

Let’s first look at using symmetric encryption.

### Symmetric Encryption

For my fourth-grade encryption system to work, my buddies and I all had to have exactly the same key to encrypt and decrypt our messages. Using the wrong key on either the sending or receiving end would result in gibberish. This system is called *symmetric encryption*. With symmetric encryption, the key used to encrypt a message is the same key used to decrypt the message. That means the sender and the receiver must both have the exact same key. This is shown in Figure 18-1.

![Figure 18-1](img/fb5404b3ce1e1e1d707f5abc39814a4a_754_0.png)

Symmetric encryption works very well. One of its key advantages is speed. It is much faster than asymmetric encryption (discussed later). However, one of the difficulties associated with symmetric encryption is how to securely distribute the key to all the parties that need to communicate with each other. For example, if you’ve ever configured a WEP key on a wireless network, you know that you must create the key on the wireless access point, copy it to a USB thumb drive, sneaker-net it to each wireless client, and paste the WEP key in the configuration of the wireless NIC. Examples of cryptographic standards that use symmetric encryption include the following:

- **Triple Data Encryption Standard (3DES)**: 3DES is commonly used by many Linux services. 3DES encrypts data in three stages. It uses either a 112-bit or a 168-bit key.
- **Advanced Encryption Standard (AES)**: AES is an improved version of 3DES. It supports 128-bit, 192-bit, and 256-bit keys.
- **Blowfish**: Blowfish uses variable key lengths up to 448 bits.

An important factor to keep in mind when selecting any encryption scheme is the number of bits used to encode the data. Older encryption schemes used only 40 or 56 bits to encode data. In today's computing world, this simply isn't strong enough. A fast PC from your local discount retail store can crack 40-bit encryption in a relatively short amount of time. When selecting an encryption scheme, you should pick one that supports a minimum of 128 bits. Basically, the longer the key, the more secure the data is.

Because of the difficulties associated with key distribution, another encryption mechanism is commonly used today called *asymmetric encryption*. Let's look at how it works next.

### Asymmetric Encryption

Unlike symmetric encryption, asymmetric encryption uses two keys instead of one: the public key and the private key. Data that has been encoded with the public key can be decoded only with the private key. Data that has been encoded with the private key can only be decoded with the public key. For this reason, asymmetric encryption is frequently referred to as public key cryptography. Rivest Shamir Adleman (RSA) and the Digital Signature Algorithm (DSA) are examples of cryptographic standards that use asymmetric encryption.

![Asymmetric Encryption Keys](img/fb5404b3ce1e1e1d707f5abc39814a4a_755_0.png)

> **NOTE** Private/public key pairs should be much longer than those used for symmetric encryption. They should be 1024 bits or longer.

This type of encryption is used to encrypt the contents of network communications as well as generate digital signatures. In a digital signature, the contents of a message aren't encrypted. Instead, the private key is used by the sender to create an encrypted hash of the message. This hash is sent along with the message to the recipient. The recipient generates its own hash of the message. Then it uses the public key to decrypt the hash sent with the message. If the hashes are the same, the recipient can be assured that the message arrived without being altered en route.

Because of its flexibility, public key cryptography is a widely used method for encrypting data. It allows you to easily scramble and send sensitive information over a public network, such as the Internet. If you've ever bought anything online from an e-commerce web site, you've used public key cryptography. When you send your credit card number, the retailer's web site should have encrypted your data and sent it using HTTPS so that prying eyes will be unable to read it.

One of the key disadvantages of asymmetric encryption is speed. Symmetric encryption is much faster than asymmetric encryption. Hence, you will frequently see implementations that use a hybrid of both mechanisms. Asymmetric encryption is used for
