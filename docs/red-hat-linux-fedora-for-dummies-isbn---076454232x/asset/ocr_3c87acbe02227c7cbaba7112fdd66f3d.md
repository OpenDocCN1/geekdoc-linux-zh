to prevent eavesdropping by encrypting the network communications to and from the web server and to identify itself to the client browser.

SSL provides encryption and ensures identification, which are described in the following two sections.

# Encryption

The mathematical process *encryption* essentially garbles information so that only those with authorization can ungarble (and read) it; encryption prevents everyone whom you don’t want to read your communications from reading it. The process of encryption and decryption requires the combination of the mathematical process named encryption algorithm and the mathematical entity cryptographic keys (keys, for short). A *key* is basically a very long number.

A description of the mathematical process of encryption is beyond the scope of this book, but suffice it to say that you need a key to encrypt information and a key to decrypt it. SSL uses a type of encryption named public-key encryption. Public-key encryption works by having the server keep a secret key and the client use a public key. The public key can be known and used by anyone and everyone; the private key must be kept secret and known only to the server.

Public-key encryption has an advantage over other encryption types because distributing public keys across a medium like the Internet is easy. It sounds counterintuitive, but public-key encryption does work.

# Identification

All the encryption in the world is useless if you’re tricked into connecting to the wrong web server. Suppose that you want to purchase a book from Amazon.com. You fire up Mozilla, connect to `www.amazon.com`, and happily enter your credit card number, expecting to receive your book the next day. It never comes.

In this scenario, some clever hacker has injected false DNS information into the Internet and your browser has even connected to `www.hackazon.com`. (Your web browser looked up the numeric IP address of Amazon.com but was deceived and received the address of the hacker’s fraudulent web server.) In this case, encryption worked-like it was supposed to and prevented other hackers from intercepting your credit card. However, it didn’t ensure that the web server was the one you thought it was, and now the hacker is enjoying a wonderful vacation in Cancun, thanks to your credit card. D’oh!

SSL identification is based on the concept of a certificate. *Certificates* contain the public key you need to set up an encrypted connection and additional information used to verify the identity of the web server. The certificate also comes with information about who created it, when it was created, and how it was created. After you obtain a certificate from the web server you’re connecting