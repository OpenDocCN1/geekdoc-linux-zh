# Building sendmail.cf At The Command Line

To create your main **sendmail** configuration file, do the following:

+   1. Log in as root on the machine you want to have as your mail server.
+   2. Set up your MC file as instructed in the section “Configuring Your **sendmail** Server At The Command Line.”
+   3. If you are using Red Hat or a Red Hat derivative distribution, type “`cd /usr/lib/sendmail-cf/cf`” to change into the directory that contains the macro file you need to edit. Otherwise, change into the directory that contains the MC file.
+   4. If you have been using a functional mail server for a while and are just making some changes, type “`cp /etc/sendmail.cf /etc/sendmail-old.cf`” to make a backup of the working configuration.
+   5. Type “`m4 .redhat.mc > /etc/sendmail.cf`” to create the new **sendmail** server configuration file.
+   6. Type “`/etc/rc.d/init.d/sendmail restart`” to stop and start the mail server, loading the new configuration.

# Tweaking Your /etc/sendmail.cf

Although a lot of people try to avoid working directly with the **sendmail** configuration file, sometimes it is worth doing so. For minor edits, it usually takes longer to work with the macro file and conversion process than to directly edit /etc/sendmail.cf.

Some of the items in this section may already have been done during other configuration phases, using the macro tools or Linuxconf. Take a moment to see whether this is the case before you start changing things.

# Adding Additional Mail Server Hostnames

To add references for other hostnames used for the mail server machine, do the following:

+   1. Log in to the mail server as root.
+   2. Type “`/vi /etc/sendmail.cf`” to open the **sendmail** configuration file.
+   3. Type “`/Cw`” and press Enter to jump down to the line that starts with:

```
```text
Cwlocalhost
```
```

+   4. Type “`$`” to jump to the end of the line, or press the End key.