> **Tip**
> 
> Use the `-s` flag with the `faxstat` command to list the contents of the send queue. To list the faxes that have arrived and are waiting in the receive queue, use the `-r` flag of the `faxstat` command.

# SETTING CLIENT DEFAULTS

Systemwide default settings for HylaFAX clients can be set using a configuration file called `hyla.conf`. The HylaFAX installation does not create this file. You must create it in the `/usr/share/fax` directory.

So far we have been specifying the hostname of the fax server when using the `sendfax` command with the `-h` flag. This is not necessary if you set a value of the default fax server in the `hyla.conf` file. Add a line like the following to `/usr/share/fax/hyla.conf`:

```
Host: orion.bwc.org
```

```
Replace orion.bwc.org with the fully qualified domain name of your fax server. Next time you use sendfax it will use this host as the default fax server host.
```

The same can also be achieved by setting the value of the environment variable FAXSERVER with the name of the fax server. In addition, a per user `.hylafax` file can be created to set default values for sendfax and other HylaFAX client programs. Check the manual page for sendfax to get a complete list of all the parameters that can be set using the `hyla.conf` or `.hylarc` files.

# SETTING UP AN EMAIL-FAX GATEWAY

The HylaFAX source distribution comes with several shell scripts and instructions on how to set up an email-fax gateway. Download the HylaFAX source distribution and unpack it in a suitable place such as `/usr/local/src`. Change your current directory to the HylaFAX source directory and look for a sub-directory called `faxmail`. Within this sub-directory three scripts are provided to set up email-fax gateways. They are the following:

+   - `faxmail/mailfax.sh-sendmail`: Suitable for systems using sendmail
+   - `faxmail/mailfax.sh-qmail`: Suitable for systems using qmail
+   - `faxmail/mailfax.sh-qmail`: Suitable for systems using qmail

We will look at the sendmail version of the script. If you are using smail or qmail, the procedure is quite similar. Follow the instructions mentioned in these script files.

Look at the different pieces involved in setting up an email-fax gateway. First, we must define a specification of how to address the message. Second, we must add an address-rewriting rule for sendmail to recognize our special address specification. Third, we must define a custom FAX mailer. And last, we have to write the mailer script.