# 10 Inspiring Raspberry Pi projects

![](bbox=[0.06, 0.1, 0.41, 0.25])

# 02 Install a lot of software

You'll want Apache software and PHP for this. Install everything you need with:

```
$ sudo apt-get install apache2 php5 php5-json php5-gd php5-sqlite curl libcurl3 libcurl4-openssl-dev php5-curl php5-gd php5-cgi php-pear php5-dev build-essential libpcre3-dev libapache2-mod-php php-apc
```

# 03 Set up PHP Accelerator

Install your accelerator with sudo pecl install apc and create an ini file for it. To do this, use sudo nano /etc/php5/cgi/conf.d/apc.ini and then add this to the file:

```
extension=apc.so
apc.enabled=1
apc.shm_size=30
```

![](bbox=[0.06, 0.48, 0.41, 0.62])

# 04 Configure file limits

Go into the Apache config file with sudo nano /etc/php5/apache2/php.ini. It's a big file, but there are two filesize options you need to find, and a third extension option you need to add as below:

```
upload_max_filesize = 2048M
post_max_size = 2200M
extension = apc.so
```

# 05 Set up SSL

First of all, you need to enable SSL in Apache; do this by using sudo nano /etc/apache2/sites-enabled/000-default and change "None" to "All" in the AllowOverride option. Follow this up with the following two commands:

```
$ sudo a2enmod rewrite
$ sudo a2enmod headers
```

# 06 Finish up with Apache

You now need to do two sets of commands: a big one which requires some info and then a restart:

```
$ sudo openssl genrsa -des3 -out server.key 1024
$ sudo openssl rsa -in server.key -out server.key.insecure
$ sudo openssl req -new -key server.key -out server.csr
$ sudo openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
$ sudo cp server.crt /etc/ssl/certs;sudo cp server.key /etc/ssl/private;sudo a2enmod ssl
$ sudo a2ensite default-ssl
$ sudo service apache2 restart
```

# 07 Download and install ownCloud

Here you have a series of commands to run that will download, unzip and install ownCloud to the right place:

```
$ wget https://download.owncloud.org/community/ownCloud-7.0.0.tar.bz2
$ sudo tar -xjf owncloud-7.0.0.tar.bz2
$ sudo cp -r owncloud /var/www
```

# 08 ownCloud permissions

Make sure your hard drive is connected and mounted as you want it. First, give webserver permission to use ownCloud:

```
$ sudo chown -R www-data:www-data /var/www/owncloud/
```

Next, use sudo nano /var/www/owncloud/.htaccess and make the same changes you did in the php.ini file above. Finally, give permissions to the location you mounted the hard drive to with:

```
$ sudo chown -R www-data:www-data [mount]
```

![](bbox=[0.55, 0.58, 0.72, 0.82])

# 09 Set up ownCloud

Open Midori and navigate to `https://[ipaddress]/owncloud` to begin the ownCloud setup process. The first thing you'll need to do is change the data location to the mount point of your external drive, which can be found in the advanced options. And you're done!

# Be inspired

Need an idea of what your next step could be? Check out our media caster tutorial and maybe you can fuses the two concepts together. Upload videos to your cloud and get them to play over your network.