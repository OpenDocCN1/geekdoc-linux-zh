# Do not alter the back ticks ( ` ) or the single quotation marks (')

Be careful not to alter the back ticks ( ` ) or the single quotation marks (') in any line in **send-mail.mc**. These symbols control the way the rm4 preprocessor converts **sendmail.mc** to **sendmail.cf**. **sendmail** will not work properly if you do not preserve these symbols.

When you restart it, **sendmail** regenerates the **sendmail.cf** file from the **sendmail.mc** file you edited:

```
# /sbin/service sendmail restart
```

Test **sendmail** with the following command:

```
$ echo "my sendmail test" | /usr/sbin/sendmail user@remote.host
```

Replace *user@remote.host* with an email address on *another system* where you receive email. You need to send email to a remote system to make sure that **send-mail** is relaying your email.

# # JUMPSTART II: CONFIGURING SENDMAIL ON A SERVER

If you want to receive inbound email sent to a registered domain that you own, you need to set up **sendmail** as an incoming mail server. This JumpStart describes how to set up such a server. This server

+   - Accepts outbound email from the local system only.
+   - Delivers outbound email directly to the recipient's system, without using a relay.
+   - Accepts inbound email from any system.

This server does not relay outbound email originating on other systems. Refer to “access: Sets Up a Relay Host” on page 680 if you want the local system to act as a relay. For this configuration to work, you must be able to make outbound connections from and receive inbound connections to port 25.

The line in **sendmail.mc** that limits **sendmail** to accepting inbound email from the local system only is

```
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```

To allow **sendmail** to accept inbound email from other systems, remove the parameter **Addr=127.0.0.1**, from the preceding line:

```
DAEMON_OPTIONS(`Port=smtp, Name=MTA')dnl
```

By default, **sendmail** does not use a remote SMTP server to relay email, so there is nothing to change to cause **sendmail** to send email directly to recipients' systems. (JumpStart I set up a **SMART_HOST** to relay email.)