# 346 Chapter 12 Sendmail Security

334 INNEDETDeuxFREJoUndurnbmnhNWItOMJNGb29Klubm9zb2Z0LMvbT4=
>>> MJGetFdsZk1YW4ImebtVLMD1NDbHZkjfyHHVSWEMGMyYNNzg2Q==
255 Authentication successful.
>>> MAIL: <craig@ani.foobirds.org> AUTH-craig@ani.foobirds.org
250 <craig@ani.foobirds.org>... Sender ok
>>> RCPT To:<craig@wren.foobirds.org>
250 <craig@wren.obobirds.org>... Recipient ok
>>> DATA
354 Enter mail, with ". on a line by itself
>>>
250 NAA01047 Message accepted for delivery
>>> QUIT
221 wren.foobirds.org closing connection

> The session in Listing 12.6 appears as it would in a verbose Sendmail session. The >>> prompt that flags client would not appear in a real SMTP protocol exchange. Additionally, the change string and response have been cut down to one line to save the trees. In reality they can be much longer.

Listing 12.6 shows the third use for the AUTH keyword. Look at the MAIL From: envelope header. The keyword AUTH appears after the sender address. The authenticated client system of mail. In effect, the source of the mail is “vouched for” by a client that the server now trusts. If the server relays this mail to another server, it will make sure to forward this validated address on with the mail.

For the DIGEST-MD5 authentication in Listing 12.6 to work, the client and server must agree on a shared secret password. The password is configured on the server using the saslpassword command as shown below:

```
[root]# saslpassword craig
Password: Let’keepthissecret!
Again (for verification): Let’keepthissecret!
```

The administrators of the server and the client must manually coordinate the password. The same password that is defined on the server using the saslpassword command must be defined on the client when the client is configured.