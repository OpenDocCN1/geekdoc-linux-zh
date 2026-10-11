The secure copy command, *scp*, works in the same way. When the connection is established, the traffic is encrypted. However, once the session is done, the connection is torn down and the encryption has ceased.

```
tigerden:/home/stripes$ scp file stripes@tigerlair.com:/user/home/stripes
stripes@tigerlair.com's password:
```

# PRETTY GOOD PRIVACY (PGP)

Because most people don’t want their *e-mail* read by anyone other than themselves, prevent other people from looking at it. This includes system administrators. Most system administrators should not be looking at your *e-mail*; however, some might have that much time on their hands. I’m not saying that all system administrators are going to be reading your *e-mail*, just be aware of what’s possible.

Pretty Good Privacy, PGP, is cool because you not only encrypt your message, but you can sign it with a digital signature. A digital signature is a hash generated from your private key that can be verified with your public key.

You can encrypt and decrypt messages, sign messages, verify signatures, and some *e-mail* programs like *elm* have PGP functionality built directly into it to sign and encrypt messages.

If you use *pgp* on your command line, it works nicely. Listing 9-2 demonstrates how I generated my key.

# **Listing 9-2: PGP key generation**

```
$ pgp -kg

Pretty Good Privacy(tm) 2.6.2 - Public-key encryption for the masses.
(c) 1990-1994 Philip Zimmermann. Phil's Pretty Good Software. 11 Oct 94
Uses the RSAREF(tm) Toolkit, which is copyright RSA Data Security, Inc.
Distributed by the Massachusetts Institute of Technology.
Export of this software may be restricted by the U.S. government.
Current time: 1998/07/20 21:36 GMT
Pick your RSA key size:
    1)  512 bits- Low commercial grade, fast but less secure
    2)  768 bits- High commercial grade, medium speed, good security
    3) 1024 bits- "Military" grade, slow, highest security
Choose 1, 2, or 3, or enter desired number of bits: 3
Generating an RSA key with a 1024-bit modulus.

You need a user ID for your public key.  The desired form for this
user ID is your name, followed by your E-mail address enclosed in
<angle brackets>, if you have an E-mail address.
For example:  John Q. Smith <12345.6789@compuserve.com>
```