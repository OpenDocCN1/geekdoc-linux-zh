
# Chapter 12 Sendmail Security

decrypted with the source's public key, proving the message came from the source. Additionally, the fact that the checksum was produced using the original content of the message means that the recipient can detect corrupted data by rerunning the checksum. This provides authentication for both the source and the content.

Secure key distribution a weakness of public key cryptography is that you must trust the source of the public key. Everything—authentication, encryption, and decryption—depends on the public key. A key obtained from a corrupted server undermines the security of everything. Some commercial outfits offer public keys on a fee basis. Most organizations use these services. Other organizations create bilateral agreements establishing trust between the organizations for the purpose of distributing keys. In effect, an organization tells its partners to trust a specific server as the source of its public keys.

The Sendmail security protocols do not define a mechanism for distributing public keys. These protocols assume that the keys have been obtained from a trusted public key server or distributed by some other mechanism.

# Sendmail Authentication

The AUTH extension to SMTP is used to authenticate the SMTP client and individual messages transmitted by the client. This extension does not encrypt messages. Instead it provides assurance that the source of the message is who it claims to be. AUTH is used to validate the client system when the system cannot be validated by its IP address—for example, when the client is a mobile system or when the client connects to the server through a third party that dynamically assigns an IP address. The keyword AUTH is used in three distinct ways.

AUTH appears in the list of keywords displayed in response to the EHLO command. When used in this way, AUTH advises the fact that the server supports the AUTH extension to SMTP and advertises the authentication methods supported by the server. We first saw this in Listing 1.2 of Chapter 1, “Internet Mail Protocols,” when the server displayed the following informational message:

250–DIGEST-MD5

This message tells the client that the server supports the AUTH extension and that it uses DIGEST-MD5. Message Digest 5 (MD5) is an encryption system that is generally used for authentication.

The list of authentication techniques advertised by the server is determined by the intersection of the techniques supported by the SASL library (libsasl) and the techniques requested by the administrator in the Sendmail configuration using the AuthMechanisms option. The AuthMechanism option is defined using CONFAUTH_MECHANISMS in the m macro configuration file—for example:

```
define(`CONFAUTH_MECHANISMS','DIGEST-MD5 CRAM-MD5')
```

This define commands the the server to use either DIGEST-MD5 or CRAM-MD5 (Challenge/Response Authentication Mode) for client authentication. With the SASL library on the server is configured for one or both of authentication techniques, that is what will be advertised in response to the EHLO command.

The client then picks an authentication technique from those that are advertised and uses the AUTH command to start the authentication process. This is the second use for the AUTH keyword. The client simply sends the command followed by the authentication techniques selected from the list of advertised techniques—for example:

```
AUTH CRAM-MD5
```

Listing 12.6 shows a more complete example of the authentication exchange between a client and a server. In Listing 12.6, the server adverts DIGEST-MD5 as the only authentication technique. The client decides to use it and responds with the necessary AUTH command. The server then encrypts the challenge string and its own authentication data, converts the encrypted response to a BASE64 string, and sends that back to the server. In Listing 12.6, the server accepts the reply and the authenticated session is off and running.

# 12.6 An Authenticated SMTP Session

```
220 wren.foobirds.org SMTP Sendmail 8.11.0/8.11.0; Mon, 18 Oct 2000
11:32 -0400
>>> EHLO ani.foobirds.org
250-w.foobirds.org Hello@ani.foobirds.org [172.16.12.1], pleased to
meet you
250-ENHANCEDSTATUSCODES
250-EXPN
250-VERB
250-8BITIME
250-SIZE
250-ONEX
250-ETRN
250-XUSR
250-AUTH DIGEST-MD5
250 HELP
>>> AUTH DIGEST-MD5
```

![](img/9639113aa446fb8976cb3d377f7aafdd_368_0.png)

334 INNTEDTeUXFREJoUundnrBmNWHtOMjNGb29kLMub9b2Z0LMnVbT4=
>>> MJGetFndSzt2KY41M11VtMD1NDHBZkjfyHHVSEGMMyYNNg2ZQ==
235 Authentication successful.
>>> MAIL From:<craig@ani.foobirds.org> AUTH-craig@ani.foobirds.org
250 <craig@ani.foobirds.org>... Sender ok
>>> RCPT To:<craig@wren.foobirds.org>
250 <craig@wren.foobirds.org>... Recipient ok
>>> DATA

354 Enter mail, with "." on a line by itself
>>>
250 NAA01047 Accepted for delivery
>>> QUIT
221 wren.foobirds.org closing connection
```

> NOTE The session in Listing 12.6 appears as it would in a verbose Sendmail session. The >>> prompt that flags client input would not appear in a real SMTP protocol exchange. Additionally, the challenge string and response have been cut down to one to save the trees. In reality they can be much longer.

Listing 12.6 shows the third use for the AUTH keyword. The MAIL From: envelope header. The AUTH appears after the sender address. The authenticated client system uses the AUTH keyword in this way to authenticate the user that sent this individual piece of mail. In effect, the source of the mail is "vouched for" by a client that the server trusts. If the server relays this mail to another server, it will make sure to forward this validated on with mail.

For the DIGEST-MD5 authentication shown in Listing 12.6 to work, the client and server must agree on a shared secret password. The password is configured on the server using the sas1password command as shown:

```
[root]# saspassword craig
Password: 'keepthissecret!'
Again (for verification): Let 'keepthissecret!'
```

The administrators of the server and the client must manually coordinate the password. The password defined on the server using the saspassword must be defined on the client.

# Configuring an Authentication Client

There are two ways that the AUTH client can communicate with your server:

- The client may run an MUA that uses your server as an MSA. Many MUAs, such as pine and Eudora, support the AUTH extension. Using this approach, the client's MUA talks directly to your server.
- The client may run Sendmail and act as an MTA. The advantage of running Sendmail on the client is that every MUA has access to the AUTH extension.

The DefaultAuthInfo options point to the file that contain the information used to authenticate the system when it acts as a client. By default, this is defined and the system does not attempt to use AUTH when acting as a client. Use confDEF_AUTH_INFO in the m4 configuration file to define a file for the AUTH data:

```
define(`confDEF_AUTH_INFO`, `/etc/mail/default-auth-info`)
```

The file can be any name you wish, /etc/mail/default-auth-info is recommended by the Sendmail developers. The file must be in a directory that can only be written by root or the TrustedUser. The file itself must be owned by root or the TrustedUser and must be readable by its own owner.

The file, default-auth-info in our example, contains four pieces of information used to authenticate the AUTH client. Explained in SASL terms, the four pieces of information are:

**Authorization identity** is this identity under which action will be taken on the remote system. This is the username that grants privileges on the remote system. For example, craig is a user ID that grants ownership privileges for every file owned by craig. The authorization identity determines the privileges.

**Authentication identity** is this username that is being authenticated by the challenge/response protocol. It does not need to be the same username as the authorization identity. However, once the authorization identity (authid) is authenticated, it is accepted as a proxy for the authorization identity and is granted the same privileges as those granted to the authorization identity. For example, assume that craig is the authorization identity and kathy is the authentication identity. After authenticating, Kathy is given ownership privileges to the files owned by craig. In terms of the DIGEST-MD5 example given above, the authentication identity should match a user name for which saspassword was used to create a password.
