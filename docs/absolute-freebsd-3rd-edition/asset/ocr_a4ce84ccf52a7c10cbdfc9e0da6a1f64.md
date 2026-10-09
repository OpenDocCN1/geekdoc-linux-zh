Some mail servers very strictly inspect relayed mail and reject inadequately forged messages. For those hosts, you'll need to use the MASQUERADE option. Masquerading gives you a couple different options for changing messages. If you use an entire email address, all mail sent via dma(8) is rewritten so it comes from that address. If you use a username with an @ sign, such as bert@, all email appears to be coming from that user at the host. A hostname on its own leaves the sending username untouched but changes the hostname.

```
MASQUERADE bert@mwl.io
```

Any messages sent from this host appear to be from Bert. Any replies will go to him. All is as it should be.

# Disable Local Delivery

Some hosts should never receive mail. No account on the host should ever get mail, not even from other local accounts. Totally disable local mail delivery by uncommenting the NULLCLIENT option.

# Secure Transport

Over the decades, the email protocol has had a whole bunch of different security measures wedged into it. Your mail server might use any or all of them. Speak to your email administrator about what your smart host requires and supports.

Enable TLS (or SSL, if your mail server is notably awful) by uncommenting the SECURETRANSFER option. You don't need to set this to a value; its mere presence turns on TLS. If your mail server needs STARTTLS, also uncomment that option. If you want to send mail even if TLS negotation fails, also uncomment OPPORTUNISTIC_TLS.

These three options all require the previous options. You can use SECURETRANSFER on its own, STARTTLS and SECURETRANSFER together, or all three. STARTTLS and SECURETRANSFER without their preceding options don't work.