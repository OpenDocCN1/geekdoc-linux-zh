
## OwnCloud 7:
Own your data

Oft' accused of having their head in the clouds, Linux Format heads for the stratosphere. Also the latest release of OwnCloud.

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_77_0.png)

Build Service provides packages for popular distributions. Instructions are available at http://owncloud.org/install. On Ubuntu 14.04, for example, you would create the file /etc/apt/sources.list.d/owncloud.list containing the line: deb http://download.opensuse.org/repositories/isv:/ownCloud:/community/xUbuntu_14.04/ apt Then (optionally) add the repo key to apt to suppress warning messages about foreign packages: wget http://download.opensuse.org/repositories/isv:/ownCloud:/community/xUbuntu_14.04/Release.key sudo apt-key add - < Release.key And finally update the package database and install a shiny (or watery?) new version of OwnCloud sudo apt-get update sudo apt-get install owncloud

## Cloud provider

As a responsible cloud host, one of your duties will be enabling and enforcing https connections. To do this you need to be in possession of a signed SSL certificate, and to tell your web server about it. (See the Generating a Self-Signed Certificate box on p.79). OwnCloud adds its own configuration file /etc/apache2/conf-available/owncloud.conf. This contains an alias that will map /owncloud on your server to its default install directory /var/www/owncloud. So navigate to https://yourserver.com/owncloud (replacing yourserver.com with your server's domain name or IP address). If you are using a self-signed certificate, then you will receive a warning about the certificate being

We've already highlighted how OwnCloud can help you evade proprietary cloud storage (see p22) but we're going to have a look at the changes in the latest and greatest version 7 of the rapidly versioning filesharing and document-collaboration tool. In fact, by the time you read this version 7.2 will be released and, as the kinks are ironed out, what's emerging is quite a remarkable product. You'll need your own server in which to house your cloud. This might be local or remote, actual or virtual, it doesn't really matter. What does matter is that, on the said server, you have a web server running that's accessible from whatever network you want to share on. If this is the internet then usual caveats about safety apply (see p16). For this tutorial we assume a working Apache setup, but the same ideas spouted here apply to Nginx or Lighttpd. Your distribution's repos might already have the latest version of OwnCloud available, but if not the lovely OpenSUSE

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_77_1.png)

Document collaboration proved to be perfectly serviceable, but we didn't really achieve productivity.

## Generating a self-signed certificate

If you have your own domain name then you can obtain a free certificate from www.startssl.com, or a paid-one from any number of other registered authorities. However, you can also generate and sign your very own certificate if you want, as follows:

```
sudo openssl req -x509 -nodes -days 365 -newkey rsa:4096 -keyout /etc/apache2/ssl/owncloud.key -out /etc/apache2/ssl/owncloud.crt
```

You will be asked for some address and company details, as well as a Common Name (which you should set to your domain name if you have one) and a contact email address. This will generate a self-signed (X.509) certificate, which will be valid for one year and will

include a 2048-bit RSA (the default) key. We need to tell your web server to use these credentials for handling connections on port 443. A standard Apache installation comes with a file /etc/sites-available/default-ssl.conf, which we can modify slightly to suit our purposes.

The <VirtualHost _default_:443> tag applies to any VirtualHost that isn't explicitly mentioned elsewhere in the block, so if you don't have any other configuration in place this is as good a place as any to add the certificate information.

You need to change the SSLCertificateFile directives as follows: SSLCertificateFile /etc/apache2/ssl/owncloud.crt then the keyfile:

```
SSLCertificateKeyFile /etc/apache2/ssl/owncloud.key
```

You should also change the ServerAdmin email address and the ServerName address to your domain name or IP address. Now enable the Apache SSL module and our new configuration, either by using the a2en(mod_site) helpers provided in Debian-based packages, or by using a good old fashioned:

```
ln -s /etc/apache2/mods-available/ssl.conf /etc/apache2/mods-enabled/
```

```
ln -s /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-enabled/
```

Restart the Apache daemon and you should be wired for SSL.

untrusted. And rightfully so, but you know that you made the certificate, and you trust yourself, so you should add a security exception here. Even though visitors won't be able to verify the server's identity (unless you somehow shared the certificate's fingerprint with them), they will at least know that the connection is encrypted.

Your first job as cloud overlord is to set up an administrator account and choose the format for the OwnCloud database. If you envisage a small cloud (such as cirrus uncinus) then SQLite will be fine, but if you have multiple users all co-operating/fighting over terribly important documents (and TPS reports) then SQLite will buckle under the strain and you will need a proper SQL database. We'll stick with SQLite for now, but note that it is possible to convert to one of the more grown up databases further down the line. Choose a suitable moniker for your admin account, use a good password and click Finish setup.

Bam! Owncloud is ready to go. You'll be invited to download the sync apps for desktop machines (Yes, there's a Linux client) and mobile devices, and instructed to connect your calendar and contacts. All in good time though. First of all we really ought to disable insecure http connections. So go to the menu in the top right and open the Admin panel. Scroll down until you find the Enforce HTTPS check box, which you should tick. Now logout and try and visit your Owncloud via http://. All going well you should be redirected to the https:// site. Safe and sound.

## Cloud is a wonderful thing

Setting up user accounts is simple: Log in as Admin, select the Users option from the top-right menu, give you and your friends usernames and passwords, and share them appropriately. Setting up groups and quotas is also done from this page, so you can stop your users from wasting storage with their Barry Manilow MP3s. It's good practice to only use the Admin account for administrative things, so use your personal account for storing and sharing your files, photos and Michael Bolton tracks. To upload a file select the Files area from the top-left menu and either click the upload button or just drag your files onto the browser window (a la Google Drive).

In previous incarnations this was limited to OpenDocument formats only. The file format voodoo is all carried out through Libre/OpenOffice, so you will need to install one of these, either on the Owncloud server you just set up or on another machine set up as a file filter server. LibreOffice is pretty big though, and it seems rather inefficient to install this on a machine where the GUI or most of its features will never be used. On Ubuntu you can install it with

```
$ sudo apt-get install libreoffice --no-install-recommends
```

to cut down on the cruft a little. Installed this way the packages only weighed in at 116MB. It's up to you to whether being able to work with obfuscated and inefficient file formats is worth this space investment – the open formats work fine without it, and you can also view PDFs in the browser too, through an adapted PDF.js viewer.

The old-style rigid Shared folder is no more, so items can be shared from anywhere in the hierarchy. Further, people you share the item with are free to move it around their own folder structure as they see fit. Users can put time limits on public shares and admins can enforce these, as well as mandate password usage. OwnCloud has always had support for external storage sources, be it (S)FTP servers, Windows

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_78_0.png)

The initial setup screen posts warnings about our self-signed certificate. High-grade encryption doesn't really help if there's a man in the middle.

Quick tip If you're important and are looking for an Enterprise grade solution for on-premises cloud storage, then checkout the commercial offering at https://owncloud.com.
