
# 36.2.1.2 Locating the SWAT Support Files

Now that you have found that **swat** is in the search path, it is easy to identify where the file is located. Here is another simple way this may be done:

```
frod0:" # whereis swat
swat: /usr/sbin/swat /usr/share/man/man8/swat.8.gz
```

If the above measures fail to locate the **swat** binary, another approach is needed. The following may be used:

```
frod0:/ # find / -name swat -print
/etc/xinetd.d/swat
/usr/sbin/swat
/usr/share/samba/swat
frod0:/ #
```

This list shows that there is a control file for **xinetd**, the internetwork super-daemon that is installed on this server. The location of the SWAT binary file is /usr/sbin/swat, and the support files for it are located under the directory /usr/share/samba/swat.

We must now check where **swat** expects to find its support files. This can be done as follows:

```
frod0:/ # strings /usr/sbin/swat | grep "/swat"
/swat/
...
/usr/share/samba/swat
```

The `/usr/share/samba/swat/` entry shown in this listing is the location of the support files. You should verify that the support files exist under this directory. A sample list is as shown:

```
jht@fromo:/ > find /usr/share/samba/swat -print
/usr/share/samba/swat
/usr/share/samba/swat/help
/usr/share/samba/swat/lang
/usr/share/samba/swat/lang/ja
/usr/share/samba/swat/lang/ja/help
/usr/share/samba/swat/lang/ja/images
/usr/share/samba/swat/lang/ja/help/welcome.html
/usr/share/samba/swat/lang/ja/images
... /usr/share/samba/swat/lang/ja/include
/usr/share/samba/swat/lang/ja/include/header.nocss.html
...
/usr/share/samba/swat/lang/tr
/usr/share/samba/swat/lang/tr/help
/usr/share/samba/swat/lang/tr/help/welcome.html
/usr/share/samba/swat/lang/tr/images
/usr/share/samba/swat/lang/tr/images/home.gif
... /usr/share/samba/swat/lang/tr/include
/usr/share/samba/swat/lang/tr/include/header.html
...
/usr/share/samba/swat/using_samba
... /usr/share/samba/swat/images
/usr/share/samba/swat/images/home.gif
... /usr/share/samba/swat/include
/usr/share/samba/swat/include/footer.html
/usr/share/samba/swat/include/header.html
jht@fromo: / >
```

If the files needed are not available, it is necessary to obtain and install them before SWAT can be used.

## 36.2.2 Enabling SWAT for Use

SWAT should be installed to run via the network super-daemon. Depending on which system your UNIX/Linux system has, you will have either an inetd- or xinetd-based system.

The nature and location of the network super-daemon varies with the operating system implementation. The control file (or files) can be located in the file `/etc/inetd.conf` or in the directory `/etc/[x]inetd.d` or in a similar location.

The control entry for the older style file might be:

```
# swat is the Samba Web Administration Tool
swat stream tcp nowait.400 root /usr/sbin/swat swat
```

A control file for the newer style xinetd could be:

```
# default: off
# description: SWAT is the Samba Web Admin Tool. Use swat \
#	to configure your Samba server. To use SWAT, \
#connect to port 901 with your favorite web browser.
service swat
{
    port = 901
    socket_type = stream
    wait = no
    only_from = localhost
    user = root
    server = /usr/sbin/swat
    log_on_failure += USERID
    disable = no
}
```

In the above, the default setting for `disable` is `yes`. This means that SWAT is disabled. To enable use of SWAT, set this parameter to `no` as shown.

Both of the previous examples assume that the `swat` binary has been located in the `/usr/sbin` directory. In addition to the above, SWAT will use a directory access point from which it will load its Help files as well as other control information. The default location for this on most Linux systems is in the directory `/usr/share/samba/swat`. The default location using Samba defaults will be `/usr/local/samba/swat`.

Access to SWAT will prompt for a login. If you log onto SWAT as any non-root user, the only permission allowed is to view certain aspects of configuration as well as access to the password change facility. The buttons that will be exposed to the non-root user are **HOME**, **STATUS**, **VIEW**, and **PASSWORD**. The only page that allows change capability in this case is **PASSWORD**.

As long as you log onto SWAT as the user *root*, you should obtain full change and commit ability. The buttons that will be exposed include **HOME**, **GLOBALS**, **SHARES**, **PRINTERS**, **WIZARD**, **STATUS**, **VIEW**, and **PASSWORD**.

### 36.2.3 Securing SWAT through SSL

Many people have asked about how to set up SWAT with SSL to allow for secure remote administration of Samba. Here is a method that works, courtesy of Markus Krieger. Modifications to the SWAT setup are as follows:

- 1. Install OpenSSL.
- 2. Generate certificate and private key.

```
root# /usr/bin/openssl req -new -x509 -days 365 -nodes -config \
    /usr/share/doc/packages/stunnel/stunnel.cnf \
    -out /etc/stunnel/stunnel.pem -keyout /etc/stunnel/stunnel.pem
```

- 3. Remove SWAT entry from [x]inetd.
- 4. Start stunnel.

```
root# stunnel -p /etc/stunnel/stunnel.pem -d 901 \
    -l /usr/local/samba/bin/swat swat
```

Afterward, simply connect to SWAT by using the URL <https://myhost:901>, accept the certificate, and the SSL connection is up.

### 36.2.4 Enabling SWAT Internationalization Support

SWAT can be configured to display its messages to match the settings of the language configurations of your Web browser. It will be passed to SWAT in the Accept-Language header of the HTTP request. To enable this feature:

- Install the proper **msg** files from the Samba source/po directory into **$LIBDIR**.
- Set your browsers language setting.

The name of the **msg** file is the same as the language ID sent by the browser. For example, *en* means English, *ja* means Japanese, *fr* means French.

If you do not like some of messages, or there are no **msg** files for your locale, you can create them simply by copying the **en.msg** files to the directory for “your language ID.msg” and filling in proper strings to each “msgstr”. For example, in *it.msg*, the **msg** file for the Italian locale, just set:

```
msgid "Set Default" msgstr "Imposta Default"
```

and so on. If you find a mistake or create a new **msg** file, please email it to us so we will consider it in the next release of Samba. The **msg** file should be encoded in UTF-8.

Note that if you enable this feature and the *display charset* is not matched in your browser's setting, the SWAT display may be corrupted. In a future version of Samba, SWAT will always display messages with UTF-8 encoding. You will then not need to set this **smb.conf** file parameter.

# 36.3 Overview and Quick Tour

SWAT is a tool that may be used to configure Samba or just to obtain useful links to important reference materials such as the contents of this book as well as other documents that have been found useful for solving Windows networking problems.

## 36.3.1 The SWAT Home Page

The SWAT title page provides access to the latest Samba documentation. The manual page for each Samba component is accessible from this page, as are the Samba3-HOWTO (this document) as well as the O'Reilly book “Using Samba.”

Administrators who wish to validate their Samba configuration may obtain useful information from the man pages for the diagnostic utilities. These are available from the SWAT home page also. One diagnostic tool that is not mentioned on this page but that is particularly useful is *ethereal*¹.

![](img/86d74c6cc862465e3a42e6dc3c90935a_632_0.png)

WARNING
SWAT can be configured to run in **demo** mode. This is not recommended because it runs SWAT without authentication and with full administrative ability. It allows changes to **smb.conf** as well as general operation with root privileges. The option that creates this ability is the *-a* flag to SWAT. *Do not use this in a production environment.*

## 36.3.2 Global Settings

The **GLOBALS** button exposes a page that allows configuration of the global parameters in **smb.conf**. There are two levels of exposure of the parameters:

- **Basic** — exposes common configuration options.
- **Advanced** — exposes configuration options needed in more complex environments.
