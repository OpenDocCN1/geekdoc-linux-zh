outgoing mail from users of virtual mail sites translates to their virtual domains, use the /etc/mail/genericstable file.

For example, suppose you have a virtual mail site called classifiedworks.com, for which you have an FTR file such as /etc/mail/classifiedworks.ftr, which has the following line:

```
sales@classifiedworks.com sheila
```

The sales@classifiedworks.com address is mapped to a local user called sheila. When Sheila sends mail using the sendmail server, you want her mail to appear as sheila@classifiedworks.com, not sheila@yourdomain.com. In such a case, create an /etc/mail/genericstable file with the following line:

```
sheila sales@classifiedworks.com
```

This reverses the content of the vusersortable file. In the spirit of keeping domain-specific information separate, you may want to create a separate reverse map file per domain. Suppose this file will have the extension .rtf (real-to-fake). After you create such a file for each domain for which you use virtual mail service, create a combined /etc/mail/genericstable file as follows:

```
touch /etc/mail/genericstable
cat *.rtf >> /etc/mail/genericstable
```

Run the make map program to create the database version of this file:

```
makemap hash /etc/mail/vusersortable < /etc/mail/vusersortable
```

In summary, for each virtual mail domain, create an FTR file that maps fake e-mail addresses to real ones, and make another file to map real addresses to fake e-mail addresses. After you make these files, combine them to create an /etc/mail/vusersortable file (for *.ftr) and an /etc/mail/genericstable file (for *.rtf). Then, run make map to create the database versions of these files. This completes the process as long as you have each of the virtual domains listed in the /etc/mail/sendmail.cw and /etc/mail/relay-domains files.