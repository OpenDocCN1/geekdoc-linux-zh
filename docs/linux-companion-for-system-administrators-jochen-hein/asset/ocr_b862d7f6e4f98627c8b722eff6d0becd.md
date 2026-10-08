# 23.1.4 Authentication

As a rule, you must identify yourself to your ISP with your user ID and password before the PPP drivers are started. the caller cannot be sure that the counterpart is indeed the ISP. Authentication in the opposite direction is seldom used (this also applies to everyday life). Thus, everybody assumes that cash machine behaves correctly, but there is no guarantee of this. If someone has set up a cache machine, it is only after entering your PIN that you notice that the machine does not distribute cash but has only been used to get hold of your PIN.

If auth is present in the option file, a PPP link can be established after authentication of the partner. Two methods can be implemented, the Cryptographic Handshake Authentication Protocol (CHAP) and the Password Authentication Protocol (PAP). If at all possible, you should use CHAP, although PAP will do.

# Cryptographic Handshake Authentication Protocol (CHAP)

The Cryptographic Handshake Authentication Protocol is based on the exchange of a 'challenge' that is encrypted with secret phrases. Each partner, no matter whether calling or called, can request authentication. By means of options, you can insist on CHAP being used, or you can allow PAP.

When partners need to authenticate themselves, they select the appropriate phrase from the file /etc/ppp/chap-secrets. Both partners need to know both phrases to be able to identify each other. Some ISDN routers support configuration of only one phrase; you can obtain more information from your provider or network administrator.

If the computer pea establishes a PPP link with corn and CHAP is used for authentication, the secrets file must be structured as in Listing 23.4.

```
|remote local secret IP address List |
pea corn "Hey, what's the password?" 192.168.3.155 |
corn pea "Ken sent me" 192.168.31.151 |
```

Listing 23.5 The file /etc/ppp/chap-secrets.

In CHAP, a 'challenge' is sent which is encrypted by means of the 'secret'. The secret is never transferred via the link. If the partner's answer is identical to the locally calculated result, the authentication was successful. The IP address field can be used to activate the connection with specific IP addresses.